# Tag

- 보통 Release할 때 사용
- tag 조회

  ~~~shell
  $ git tag
  v1.0.0
  v1.0.1
  v1.1.0
  ~~~~

- pattern 사용하여 tag 조회
  - 단순히 모든 tag 목록을 확인하기 위해 git tag 명령을 실행했을 때 -l 또는 --list 옵션이 적용된 것과 동일한 결과가 출력됨
  - 하지만 wildcard를 사용하여 tag 목록을 검색하는 경우에는 반드시 -l 또는 --list 옵션을 같이 써 줘야 함

    ~~~shell
    $ git tag -l 'v1.1.*'
    v1.1.0
    ~~~

- tag의 종류
  1. Annotated
     - tag 명령을 실행할 때 -a 옵션 추가하여 생성
     - -m 옵션으로 태그를 저장할 때 메시지를 함께 저장 가능
     - 명령을 실행할 때 메시지를 입력하지 않으면 Git은 편집기를 실행시킴

       ~~~shell
       $ git tag -a v1.4 -m "my version 1.4"
       $ git tag
       v0.1
       v1.3
       v1.4
       ~~~  

     - git show 명령으로 태그 정보와 커밋 정보 모두 확인 가능

        ~~~shell
        $ git show v1.0.0
        tag 1.0.0
        Tagger: jaeho-jang <jaehojang@nate.com>
        Date:   Thu Apr 15 10:34:31 2021 +0900

        tag 1.0.0

        commit 946b875f23c763ce14f597ae20969f5bbeb4b49f (HEAD -> 15.3.2, tag: 1.0.0, origin/15.3.2)
        Author: jaeho-jang <jaehojang@nate.com>
        Date:   Tue Apr 13 17:44:55 2021 +0900

            Prevent to click other banks

            * 국민, 광주 제외한 은행들은 선택 불가하게 수정

        diff --git a/lib/apis/index.js b/lib/apis/index.js
        ...
        ~~~

  2. Lightweight
     - Lightweight tag는 기본적으로 파일에 commit checksum을 저장하는 것뿐임
     - 다른 정보는 저장하지 않음
     - tag 생성 시 -a, -s, -m 옵션을 사용하지 않음 (이름만 달아줄 뿐)

        ~~~shell
        $ git tag v1.4-lw
        $ git tag
        v0.1
        v1.3
        v1.4
        v1.4-lw
        v1.5
        ~~~

     - 이 tag에 git show를 실행하면 별도의 태그 정보 확인 불가
     - 단순히 commit 정보만 보여줌

        ~~~shell
        $ git show v1.0.0
        commit 946b875f23c763ce14f597ae20969f5bbeb4b49f (HEAD -> 15.3.2, tag: 1.0.0, origin/15.3.2)
        Author: jaeho-jang <jaehojang@nate.com>
        Date:   Tue Apr 13 17:44:55 2021 +0900

        Prevent to click other banks
            
        * 국민, 광주 제외한 은행들은 선택 불가하게 수정

        diff --git a/lib/apis/index.js b/lib/apis/index.js
        ...
        ~~~

- tag 원격 저장소에 올리기
  - 특정 tag 지정

    ~~~shell
    git push origin 1.0.0
    ~~~

  - 모든 tag

    ~~~shell
    git push origin --tags
    ~~~

- tag 삭제
  - local tag (-d 옵션 사용)

    ~~~shell
    git tag -d 1.0.0
    ~~~

  - remote tag (':' 사용)

    ~~~shell
    git push origin :1.0.0
    ~~~
