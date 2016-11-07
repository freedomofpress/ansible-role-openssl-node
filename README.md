openssl_node
=========

Utilizes a pre-existing CA certificate stored in a variable file to spin-off a
new signed node certificate and copy that over to box.


Requirements
------------

A pre-existing CA certificate keypair must exist in a variable file in the
following format:

```yaml
certificate_authority:
    arbitrary_ca_name:
      pub: >
        asdiaodadiadoaidapodiaodadi
        asdiaodadiadoaidapodiaodadi
        asdiaodadiadoaidapodiaodadi
      private: >
        asdiaodadiadoaidapodiaodadi
        asdiaodadiadoaidapodiaodadi
        asdiaodadiadoaidapodiaodadi
```

Here is the rest of the available variables:

```yaml
just_ca_pub: false
openssl_node_bit_length: 4096
openssl_node_name: "{{ ansible_fqdn }}"
openssl_node_expiration: 365

## should change the following for production
openssl_node_ca_name: "arbitrary_ca_name"
openssl_node_ca_creds: "test_ca"

openssl_node:
  name: "{{ openssl_node_name }}"
  bit_length: "{{ openssl_node_bit_length }}"
  pub_dst: /etc/ssl/certs
  priv_dst: /etc/ssl/private
  local_tmp: ./tmp

openssl_node_pkgs:
  - openssl

openssl_node_ca:
  use: default_ca_name

# Should also change for production
ca_cert:
  city: San Francisco
  state: CA
  country: US
  org: Freedom of the Press Foundation
  ou: DevOps
  email: sysadmin@freedom.press

ca_cert_sign:
  ca_pub_key: "{{ certificate_authority[openssl_node_ca_name].pub }}"
  ca_priv_key: "{{ certificate_authority[openssl_node_ca_name].private }}"
```

License
-------

MIT

