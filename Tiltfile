# OS Identification
gradlew = "./gradlew"
expected_ref = "$EXPECTED_REF"
if os.name == "nt":
  gradlew = "gradlew.bat"
  expected_ref = "%EXPECTED_REF%"

# Build
custom_build(
    # Name of the container image
    ref = 'edge-service-1',
    # Command to build the container image
    #command = './gradlew bootBuildImage --imageName $EXPECTED_REF',
    command = gradlew + ' bootBuildImage --imageName ' + expected_ref,
    # Files to watch that trigger a new build
    deps = ['build.gradle', 'src']
)

# Deploy
k8s_yaml(['k8s/deployment.yml', 'k8s/service.yml'])
#k8s_yaml(kustomize('k8s'))

# Manage
k8s_resource('edge-service-1', port_forwards=['9000'])