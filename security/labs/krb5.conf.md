[libdefaults]
default_realm = JASZOK.DE
dns_lookup_kdc = false
dns_lookup_realm = false
ticket_lifetime = 86400
renew_lifetime = 604800
forwardable = true
default_tgs_enctypes = rc4-hmac
default_tkt_enctypes = rc4-hmac
permitted_enctypes = rc4-hmac
udp_preference_limit = 1
kdc_timeout = 3000
[realms]
JASZOK.DE = {
kdc = ec2-52-59-196-39.eu-central-1.compute.amazonaws.com
admin_server = ec2-52-59-196-39.eu-central-1.compute.amazonaws.com
}
