# 빌드
custom_build(
    # 컨테이너 이미지으 이름
    ref = 'catalog-service',
    # 컨테이너 이미지를 빌드하기 위한 명령
    command = './mvnw spring-boot:build-image -DimageName=$EXPECTED_REF',
    # 새로운 빌드를 시작하기 위해 지켜봐야 하는 파일
    deps = ['pom.xml', 'src']
)

# 배포
k8s_yaml(['k8s/deployment.yml', 'k8s/service.yml'])

# 관리
k8s_resource('catalog-service', port_forwards=['9001'])
