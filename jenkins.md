# Jenkins란?

jenkins는 소프트웨어 개발 시 지속적으로 통합 서비스를 제공해주는 CI 툴이다.

여기서 지속적으로 통합을 서비스한다라는 뜻은 파이프라인을 통해 task들을 동기적 혹은 병렬적으로 실행시킴으로 써 

master branch로 marge 될 때 unit test, build, static code Analysis 등을 실행할 수 있도록 도와주는 역할을 하고 있다.

젠킨스는 DSL(Domain-Specific Language)와 그루비를 사용한다.
## 젠킨스와 그루비
젠킨스는 오랜 시간 동안 그루비 엔진을 포함해왔다. 이는 웹 인터페이스에서 불가능한 접근 및 기능과 깊은 수준의 스크립트 작업을 지원하기 위해 사용되었다.

# Jenkinsfile
젠킨스 파일은 DSL 스크립트를 사용하여 젠킨스 잡을 실행시킬 수 있고, 변경 추적과 분석이 가능해진다.

젠킨스는 Jenkinsfile이 있으면 이를 읽어서 코드를 수행한다. 

젠킨스는 보통 gradle을 통해 정의되어 실행되고 gradle에 의해 에러처리가 되는 일명 스크립트 방식의 파이프라인(pipelines-as-code)으로 처리되었다.

하지만 젠킨스 버전이 올라가면서 빌드 후 처리, 에러 확인, 상태 기반 알림 전달 등 젠킨스에서 가능해졌다.

```jenkinsfile
pipeline {
    agent any
    stages {
        stage('Source'){
            git brach : 'test', url: 'git@diyvb:repos/gradle-greetings'
            stash name : 'test-sources', includes: 'build,gradle,/src/test'
        }
        stage('Build'){
            
        }
    }
}
```
## jenkins configure
### pipeline
파이프 라인은 생성하는 역할을 담당한다. 파이프라인은 스크립트 방식으로 작성할 수 있으며, 서술적 방식으로 작성할 수 있다.

### folder
폴더는 여러 프로젝트를 하나로 묶는 방법이다. 폴더는 실제 운영체제의 폴더와 유사하다.

폴더의 경로는 프로젝트 경로의 일부가 된다.

### github organization
몇몇 소스 관리 플랫폼은 저장소를 조직 저장소로 묶는 기능을 제공한다.

젠킨스의 통합 기능은 사용자가 젠킨스 파이프라인 스크립트를 jenkinsfile 형태로 조직 저장소에 저장해 이를 기반으로 실행될 수 있게 지원한다.

현재는 github와 bitbucket의 조직 저장소가 지원되고, 다른 것들은 지원 예정이다.

### multibranch pipeline
멀티브랜치 파이프라인 타입의 프로젝트에서 젠킨스는 Jenkinsfile을 빌드 스크립트로 활용하게 된다. 

jenkinsfile을 포함하고 있는 새로운 브랜치가 프로젝트에 생성되면 젠킨스는 자동으로 해당 브랜치를 위한 새로운 젠킨스 프로젝트를 생성한다.

이 프로젝트는 깃 혹은 서브버전 저장소에 적용될 수 있다.

