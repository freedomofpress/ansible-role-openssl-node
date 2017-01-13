openssl_node
=========

Utilizes a pre-existing CA certificate stored in a variable file to spin-off a
new signed node certificate and copy that over to box.


Requirements
------------

A pre-existing CA certificate keypair must exist in a variable file in the
following format:

```yaml
openssl_node_certificate_authority:
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
openssl_node_only_ca: false
openssl_node_bit_length: 4096
openssl_node_name: "{{ ansible_fqdn }}"
openssl_node_expiration: 365
openssl_node_ca_name: "name_of_ca_cert" # see `openssl_node_certificate_authority`
openssl_node_ca_creds: "test_ca"

openssl_node:
  name: "{{ openssl_node_name }}"
  bit_length: "{{ openssl_node_bit_length }}"
  pub_dst: /etc/ssl/certs
  priv_dst: /etc/ssl/private
  local_tmp: "./tmp/{{ ansible_fqdn }}"

openssl_node_pkgs:
  - openssl

openssl_node_ca:
  use: default_ca_name

openssl_ca_cert_details:
  city: San Francisco
  state: CA
  country: US
  org: Freedom of the Press Foundation
  ou: DevOps
  email: sysadmin@freedom.press

# Swap in your CA cert here and stick in an ansible vault
openssl_node_certificate_authority:
  name_of_ca_cert:
    pub: |
      [ .............. ]
    private: |
      [ .............. ]

openssl_node_ca_cert_sign:
  ca_pub_key: "{{ openssl_node_certificate_authority[openssl_node_ca_name].pub }}"
  ca_priv_key: "{{ openssl_node_certificate_authority[openssl_node_ca_name].private }}"
```

License
-------

MIT

