# letsencrypt

	windows executable file: le32.exe can be found on the following repository:
	https://github.com/do-know/Crypt-LE/releases

To ensure a straight forward process please do the following Pre-Staging steps:


Go to your Domain DNS Zone and add the following records without values:
	
	Record Type: TXT
	Name:		 _acme-challenge
	
	Record Type: TXT
	Name:		_acme-challenge.www
	
OR

If you have an existing TXT record on your DNS Zone you can add 2 additional lines example:

	Record Type" TXT
	Name:		@
	Value: 		your existing txt record values
	
	Record Type: TXT
	Name:		 _acme-challenge.your_domain_name=challenge_value_requested_by_Lets_Encrypt
	
	Record Type: TXT
	Name:		_acme-challenge.www.your_domain_name=challenge_value_requested_by_Lets_Encrypt
	
Your record should look something like this:

	_acme-challenge.your_domain_name=nAESxPeYEf2C-Wrm0uEO-HDs8La5HxmFladKfBOxasE
	_acme-challenge.www.your_domain_name=rpyL3-jF3wMk9DDlInmywd5bh-VU0FJWysZRcXARQDc
	v=spf1 include:spf.some_value.some_value.value -all
	
To be sure, the records are working as expected, please run the following commands in windows:

	ipconfig /flushdns = This is to flush your DNS cache
	nslookup -q=TXT _acme-challenge.your_domain_name
	nslookup -q=TXT _acme-challenge.www.your_domain_name
	
You should see a response like this:

	Non-authoritative answer:
	_acme-challenge.your_domain_name   text =

        "nAESxPeYEf2C-Wrm0uEO-HDs8La5HxmFladKfBOxasE"
		

	Non-authoritative answer:
	_acme-challenge.www.your_domain_name       text =

        "rpyL3-jF3wMk9DDlInmywd5bh-VU0FJWysZRcXARQDc"

You can also run the command adding a custom DNS server, let's say OpenDNS:

	nslookup -q=TXT _acme-challenge.www.your_domain_name 208.67.222.222
	nslookup -q=TXT _acme-challenge.your_domain_name 208.67.222.222

Please be sure to test the steps above, since if for any reason the dns server is not reachable you can't generate the cert.


Now let's start with the certificate generation.

1- Create a folder on your computer to place the files that you'll be working with.

2- Copy le32.exe in the folder.  If you already have a CSR created, please add it to the folder too.

3- Open a windows cmd console and change to the directory where you placed le32.exe

4- Fill out the information below with your values, replacing only <values>:

	le32.exe 
	--key <key_file_name>.key
	--csr <csr_file_name>.csr
	--crt <domain_certificate_name_output>.crt
	--email <"your@emailaddress">
	--domains  "<*.your_domain_name.extesion>" 
	--handle-as dns 
	--api 2 
	--live
	--generate-missing

5- Converted to a single line:

	le32.exe --key <key_file_name>.key --csr <csr_file_name>.csr --crt <domain_certificate_name_output>.crt --email <"your@emailaddress"> --domains  "<*.your_domain_name.extesion>" --handle-as dns --api 2 --live --generate-missing
	
6- The application will ask you to add the values to the previously created TXT Records.  Please make sure that you follow the 
   previous steps (Creating the TXT DNS Records).
   
7- If everything is fine, you should have your new certificate generated on your folder.


Tips:

After the process completion, please import your certificate to your "localmachine" personal store.  In case that it doesn't have a private key to export it, please use the following procedure:

1- After the import, open the certificate and click on the "details" tab.

2- Look for the "Serial Number" and copy to another location.

3- Run the following command from a windows cmd(admin):
	
	Command:
	
		certutil -repairstore my "SerialNumberofyourCertificate" ----and yes, the word "my" must be there is not a typo-----
	
4- You should have a private key to export now.


Links:

For feedback and bug reports:
	
	[ https://ZeroSSL.com | https://Do-Know.com ]
	
For ACME Client Implementations:

	https://letsencrypt.org/docs/client-options/
	
For Let's Encrypt Documentation:
	
	https://letsencrypt.org/docs/

For online certificate issuance with UI (Please not wildcard's can't be generated using this method yet):

	https://zerossl.com/free-ssl/#crt
	
To verify certificate issuance (COMODO Tool):

	https://crt.sh/
	
Win32/64 Portable ZeroSSL client for Let's Encrypt:

	https://github.com/do-know/Crypt-LE/releases

	







	
	
		
 
