FROM registry.ci.openshift.org/ocp/builder:rhel-9-golang-1.22-openshift-4.18
COPY . /go/src/github.com/openshift/csi-driver-nfs
RUN cd /go/src/github.com/openshift/csi-driver-nfs && \
    go build -o /go/src/github.com/openshift/csi-driver-nfs/nfsplugin cmd/nfsplugin/main.go

FROM registry.ci.openshift.org/ocp/4.18:base-rhel9

COPY --from=0 /go/src/github.com/openshift/csi-driver-nfs/nfsplugin /usr/bin/

RUN yum -y install nfs-utils && yum -y install jq && yum clean all

ENTRYPOINT ["/usr/bin/nfsplugin"]
