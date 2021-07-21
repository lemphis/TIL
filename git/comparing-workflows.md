# 협업 방법론 비교 (Comparing Workflows)

1. Centralized Workflow
    - master branch 하나로 모든 개발이 이루어짐(단순함)
    - 기능상 여러 버전(bugfix, hotfix, release, develop)을 구별하지 않음
    - 단점
      - 서비스 배포 이후 관리가 어려움
      - conflict가 일어날 확률이 높음
      - master branch가 더러워짐
2. Feature Branch Workflow
    - feature branch를 만들어 개발하고 master에 merge하는 방식
    - 단점
      - 서비스 배포 이후 관리가 어려움
      - conflict가 일어날 확률이 높음
      - 처음부터 명확히 feature를 구분하지 않을 경우 결국 사람 당 1개의 branch를 만들어 사용할 확률이 높음
      - feature 명명 기준이 달라 혼란이 올 수 있음
3. Gitflow Workflow
    - master, develop branch는 사라지지 않는 기본 branch
    - feature, release, hotfix는 필요할 때 만들었다가 삭제
    - 새 기능 개발 시 과정
      1. 원격 develop branch에서 feature/*** branch 생성 (ex. feature/login_layout)
      2. feature/***에서 작업 진행
      3. develop branch로 pull request 생성
      4. 관리자가 pull request 확인 후 rebase & push
      5. 해당 feature branch 삭제
4. Forking Workflow
    - 프로젝트 규모가 크거나 어떠한 기준에 따라 잘 분리되어 있을 때 사용하면 좋음
    - 과정
      1. 대표 중앙 저장소(upstream)가 있고 모든 개발자들은 이 대표 저장소를 fork하여 자신의 원격 저장소(origin)를 만듬
      2. 작업은 모두 fork한 저장소에서 진행
      3. 대표 저장소에 merge 요청(pull request)를 보냄
    - 단점
      - git을 처음 사용하는 사람의 경우 workflow를 이해하기가 다른 flow보다 상대적으로 어려움
      - 작업 상황을 자주(짧은 주기로) 리뷰하기가 쉽지 않음(통일된 관리가 어려움)

> cf. https://www.atlassian.com/git/tutorials/comparing-workflows