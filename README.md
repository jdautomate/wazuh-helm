# wazuh-helm
Helm chart for wazuh - mostly taken from wazuh kubernetes repo and converted to helm.

# SAML
saml auth is added to elastic config.yml and kibana.yml - if using internalusers for authentication, remove those saml lines. 
Security plugin must be ran in order for the info to be indexed.

sample command: bash /usr/share/elasticsearch/plugins/opendistro_security/tools/securityadmin.sh -cd /usr/share/elasticsearch/plugins/opendistro_security/securityconfig/ -icl -key /usr/share/elasticsearch/config/admin-key.pem -cert /usr/share/elasticsearch/config/admin.pem -cacert /usr/share/elasticsearch/config/root-ca.pem -nhnv

# Secrets
Most of the secrets are templates only, generate certs per instructions from wazuh.
https://documentation.wazuh.com/current/deploying-with-kubernetes/kubernetes-conf.html

# Network
Set to create 1 NLB and 1 ELB in AWS.
NLB:
  elasticsearch - port 9200
  wazuh-master - port 1515, 55000 (api)
  wazuh-worker - port 1514
ELB:
  kibana - port 443
All of these load balancers can be changed via the annotations, however after a lot of experimenting this is what worked best.
