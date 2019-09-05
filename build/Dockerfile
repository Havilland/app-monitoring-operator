FROM quay.io/operator-framework/ansible-operator:v0.10.0

USER 0

RUN yum -y install python2-passlib

USER 1001

COPY watches.yaml ${HOME}/watches.yaml

COPY roles/ ${HOME}/roles/

COPY playbooks/ ${HOME}/playbooks/
