# gateway-3.0.1-Intermountain
Fork of project from Direct

This project was created to fix a bug found in the Direct Reference implementation code. The bug deals with the processing of Direct messages.
There is an SMTP agent class that gets initialized to process Direct messages. It contains a list of "public certificate resolvers". There
 is a refresh setting in "gateway.properties" to refresh settings in this class (XMLSmtpAgentConfig.class). Every time this class was getting refreshed the list 
 of "public cert resolvers" was NOT getting cleared out. It kept growing bigger each time this was refreshed. It refreshed every 5 minutes, so over time this consumes 
 a lot of memory and when a DNS certificate for a receipient cannot be found, this causes the error logs to fill up because it logs an 
 error message for EACH public cert resolver in the list. The fix was to clear out this list when the SMTP agent class is refreshed.
