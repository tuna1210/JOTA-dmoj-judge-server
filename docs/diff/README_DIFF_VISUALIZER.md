# JOTA diff visualizer

## introduction
* 유저 `Output`과 정답 `Output`에 대해 `diff`를 수행하여 그 결과를 시각적으로 보여줍니다.
* 라이브러리는 [google/diff-match-patch](https://github.com/google/diff-match-patch)을 사용하였습니다.

## How it works
### On Judge (Server)
* **dmoj/graders/standard.py**
    * `extended_feedback`을 통해 `Answer Output`을 `Site`로 보냅니다.

### On Site (Client)
* **judge/views/submission.py**
    * `group_test_cases`에서 `cases`에 대한 루프마다 두 `output`의 `diff`결과를 연산하여 `diff[]`에 각 `case`의 결과를 저장하고 리턴합니다.
    * `group_test_cases`에서 리턴한 `diff`를 `context`에 `'diff_result'`를 키로 갖도록 넣습니다.
    * `diff_match_patch`에서 `import error` 발생 시 아래 구문 추가해서 해소 가능
        ```
        import sys
        sys.path.append('/home/ubuntu/jota/dmojsite/lib/python3.8/site-packages')
        from diff_match_patch import diff_match_patch
        ```
* **status_testcases.html**
    * `view`에서 받은 `diff_result`를 `patch`에 알맞게 보여줍니다.

## How to change diff option
* cleanupSemantics 메소드를 통해 diff를 단어 단위로 적용할 수 있다. 현재는 적용 되어있지 않다. [참고](https://github.com/google/diff-match-patch/wiki/API)

## FrontEnd Document
[Link](https://github.com/minshxxx/JOTA-dmoj-online-judge/blob/master/docs/FrontVisualization.md)