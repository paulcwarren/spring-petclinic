load('.tanzu/tanzu_live_reload.py', 'tanzu_live_reload')
allow_k8s_contexts('eduk8s')

tanzu_live_reload(k8s_object="spring-petclinic",
              manifest=["config/workload.yaml"],
              image="harbor-repo.vmware.com/kontinuedemo/spring-petclinic",
              deps=['target/classes'],
              live_update=[
                sync('target/classes', '/workspace/BOOT-INF/classes'),
              ])
