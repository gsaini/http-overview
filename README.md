# http-overview
HyperText Transfer Protocol (HTTP)



# Agenda

  1. HTTP Overview & how it works (https://flaviocopes.com/http-request/)
  
     ## DNS LOOKUP PHASE
      The browser starts the DNS lookup to get the server IP address.

      The domain name is a handy shortcut for us humans, but the internet is organized in such a way that computers can look up the exact location of a server through its IP address, which is a set of numbers like 222.324.3.1 (IPv4).

      First, it checks the DNS local cache, to see if the domain has already been resolved recently.

      Chrome has a handy DNS cache visualizer you can see at chrome://net-internals/#dns

      If nothing is found there, the browser uses the DNS resolver, using the gethostbyname POSIX system call to retrieve the host information.

      ### GETHOSTBYNAME
      
      gethostbyname first looks in the local hosts file, which on macOS or Linux is located in /etc/hosts, to see if the system provides the information locally.

      If this does not give any information about the domain, the system makes a request to the DNS server.

      The address of the DNS server is stored in the system preferences.

      Those are 2 popular DNS servers:

      `8.8.8.8: the Google public DNS server`
      
      `1.1.1.1: the CloudFlare DNS server`
      
      Most people use the DNS server provided by their internet provider.

      The browser performs the DNS request using the UDP protocol.

      TCP and UDP are two of the foundational protocols of computer networking. They sit at the same conceptual level, but TCP is connection-oriented, while UDP is a connectionless protocol, more lightweight, used to send messages with little overhead.

      How the UDP request is performed is not in the scope of this tutorial

      The DNS server might have the domain IP in the cache. It not, it will ask the root DNS server. That’s a system (composed of 13 actual servers, distributed across the planet) that drives the entire internet.

      The DNS server does not know the address of each and every domain name on the planet.

      What it knows is where the top-level DNS resolvers are.

      A top-level domain is the domain extension: .com, .it, .pizza and so on.

      Once the root DNS server receives the request, it forwards the request to that top-level domain (TLD) DNS server.

      Say you are looking for flaviocopes.com. The root domain DNS server returns the IP of the .com TLD server.

      Now our DNS resolver will cache the IP of that TLD server, so it does not have to ask the root DNS server again for it.

      The TLD DNS server will have the IP addresses of the authoritative Name Servers for the domain we are looking for.

      How? When you buy a domain, the domain registrar sends the appropriate TDL the name servers. When you update the name servers (for example, when you change the hosting provider), this information will be automatically updated by your domain registrar.

      Those are the DNS servers of the hosting provider. They are usually more than 1, to serve as backup.

      For example:


      ``ns1.dreamhost.com``
      
      ``ns2.dreamhost.com``
      
      ``ns3.dreamhost.com``
      
      The DNS resolver starts with the first, and tries to ask the IP of the domain (with the subdomain, too) you are looking for.

      That is the ultimate source of truth for the IP address.

      Now that we have the IP address, we can go on in our journey.
      
      
  2. HTTP Headers
  3. HTTP Methods - GET, POST, PUT, DELETE, OPTION, HEAD etc.
  4. HTTP Authentication
  5. HTTP StatusCode & overview, error handling - Demo
  6. Cookies
  7. Cache
  8. Content Compression - Gopal
  9. Https - Krishank
  10. Http2 & Future draft - Krishank
  11. Ajax, Cross domain & jsonp
  12. Q&A
