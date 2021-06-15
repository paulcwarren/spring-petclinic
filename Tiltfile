load('.tanzu/tanzu_live_reload.py', 'tanzu_live_reload')
allow_k8s_contexts('eduk8s')

local_resource(
  'spring-petclinic-compile',
  './mvnw -Dmaven.test.skip=true -Dspring-boot.repackage.excludeDevtools=false package && ' + 
    'rm -rf target/jar-staging && ' +
    'unzip -o target/spring-petclinic-*.jar -d target/jar-staging && ' +
    'rsync --delete --inplace --checksum -r target/jar-staging/ .build',
  deps=['src', 'pom.xml'])

tanzu_live_reload(k8s_object="spring-petclinic",
              manifest=["config/workload.yaml"],
              image="harbor-repo.vmware.com/kontinuedemo/spring-petclinic",
              resource_deps=["spring-petclinic-compile"],
              deps=['.build/'],
              live_update=[
                sync('.build/BOOT-INF/classes', '/workspace/BOOT-INF/classes'),
                sync('.build/META-INF', '/workspace/META-INF'),
              ])
