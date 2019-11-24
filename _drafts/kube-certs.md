Kubernetes Certificates, explained

First, go read Julia Evans' excellent blog post from a couple years back: https://jvns.ca/blog/2017/08/05/how-kubernetes-certificates-work/.

## CAs

Let's look at CAs first.

## API server arguments

```
--kubelet-certificate-authority string    Path to a cert file for the certificate authority.
--kubelet-client-certificate string       Path to a client cert file for TLS.
--kubelet-client-key string               Path to a client key file for TLS.
```

## kubelet arguments

```
--client-ca-file string                   If set, any request presenting a client certificate signed by one of the authorities in the client-ca-file is authenticated with an identity corresponding to the CommonName of the client certificate.
--tls-cert-file string                    File containing x509 Certificate used for serving HTTPS (with intermediate certs, if any, concatenated after server cert). If --tls-cert-file and --tls-private-key-file are not provided, a self-signed certificate and key are generated for the public address and saved to the directory passed to --cert-dir.
--tls-private-key-file string             File containing x509 private key matching --tls-cert-file.
```