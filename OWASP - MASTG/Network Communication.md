---
{"dg-publish":true,"permalink":"/src/site/notes/src/site/notes/src/site/notes/src/site/notes/main/cs/owasp-mastg/network-communication/"}
---






# ==Default Configurations==

```Java
<base-config cleartextTrafficPermitted="false">
		<trust-anchors>
				<certificates src="system" />
		</trust-anchors>
</base-config>

<base-config cleartextTrafficPermitted="true">
		 <trust-anchors>
					<certificates src="system" />
		 </trust-anchors>
</base-config>

<base-config cleartextTrafficPermitted="true">
		<trust-anchors>
				<certificates src="system" />
				<certificates src="user" />
		</trust-anchors>
</base-config>
```

# ==Certificate Pinning==

```XML
<?xml version="1.0" encoding="utf-8"?>
<network-security-config>
		<domain-config>
				Use certificate pinning for OWASP website access including sub domains
				<domain includeSubdomains="true">owasp.org</domain>
				<pin-set expiration="2018/8/10">

				<!-- Hash of the public key (SubjectPublicKeyInfo of the X.509 certificate) of
the Intermediate CA of the OWASP website server certificate -->
		
				<pin digest="SHA-256">YLh1dUR9y6Kja30RrAn7JKnbQG/uEtLMkBgFF2Fuihg=</pin>
				<!-- Hash of the public key (SubjectPublicKeyInfo of the X.509 certificate) of
the Root CA of the OWASP website server certificate -->

				<pin digest="SHA-256">Vjs8r4z+80wjNcr1YKepWQboSIRi63WsWXhIMN+eWys=</pin>
			</pin-set>
		</domain-config>
	</network-security-config>
```

# ==Libraries and WebViews==

```Java
OkHttpClient client = new OkHttpClient.Builder()
			.certificatePinner(new CertificatePinner.Builder()
						.add("example.com", "sha256/UwQAapahrjCOjYI3oLUx5AQxPBR02Jz6/E2pt0IeLXA=")
						.build())
			.build();

WebView myWebView = (WebView) findViewById(R.id.webview);
myWebView.setWebViewClient(new WebViewClient(){
			private String expectedIssuerDN = "CN=Let's Encrypt Authority X3,O=Let's Encrypt,C=US;";

			@Override
			public void onLoadResource(WebView view, String url) {

//From Android API documentation about "WebView.getCertificate()":
//Gets the SSL certificate for the main top-level page
//or null if there is no certificate (the site is not secure).
//
//Available information on SslCertificate class are "Issuer DN", "Subject DN" and validity date helpers

			SslCertificate serverCert = view.getCertificate();
			if(serverCert != null){
//apply either certificate or public key pinning comparison here
//Throw exception to cancel resource loading...
					}
			 }
		}
});
```