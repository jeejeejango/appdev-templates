## OpenShift AppDev Templates

### [Gogs](https://gogs.io/)
[OpenShiftDemos](https://github.com/OpenShiftDemos/gogs-openshift-docker) provide the Gogs OpenShift template based 
on custom build docker image. 

This templates uses the images from [docker.io/gogs/gogs](https://hub.docker.com/r/gogs/gogs). You will need to enable SCC for 
gogs service account:

```bash
oc adm policy add-scc-to-user anyuid system:serviceaccount:devops:gogs
```
where devops is the installed projects/namespaces

### [SonarQube](https://www.sonarqube.org/)
[Cingulara/openshift-templates](https://github.com/Cingulara/openshift-templates) provides SonarQube template basesd persistent storage. 

This templates update to OpenShift 4.x with Postgresql updated to min 9.6. As SonarQube uses ElasticSearch, 
```yaml
tuned.openshift.io/elasticsearch: ""
```
is added based on this [blog](https://developers.redhat.com/blog/2019/11/12/using-the-red-hat-openshift-tuned-operator-for-elasticsearch/).

For disconnected installation, you will need to download the plugins manually as reference in SonarQube [documentation](https://docs.sonarqube.org/latest/setup/install-plugin/).

You will need to rsh to SonarQube pod:
```bash
oc rsh sonarqube-xxx-xxx
```

Validate and create plugins folder if it is not created in /opt/sonarqube/extensions. Then copy the downloaded jar file to Bastion host, and rsync to plugins folder
```bash
oc rsync ./ sonarqube-xxx-xxx:/opt/sonarqube/extensions/plugins
```

### [Sonatype Nexus3](https://www.sonatype.com/nexus-repository-oss)
[OpenShiftDemos/nexus](https://github.com/OpenShiftDemos/nexus) provided Nexus3 templated based on persistent storage. A min of 5GB is required for latest version.
