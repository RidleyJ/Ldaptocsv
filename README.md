# Ldaptocsv
Python script to turn a file with LDIF (-LLL) ldapsearch results into a tabular format


BEFORE running the python script, you will need ldapsearch results.  First, use an input file called inputfilter.txt (see inputfilter.txt for an example of mine).  

I am going to do an ldapsearch with -LLL so I don't get any comments or anything, only the straight up result text.  I have dc=umich, dc=edu as the base because I'm at UM.  displayName bit is the only field I want to return in my result file, but feel free to include whichever ones you want.  They will eventually turn into columns in your csv.  The output of the query gets put into ldapresults.txt.

With all of that being said, I open bash and run the following command:


  ldapsearch -LLL -f inputfilter.txt -x -H <yourldaphost> -b "dc=umich,dc=edu" -s sub "(|(%s))" displayName > ldapresults.txt
  

Once that is done, I can run the python script.  

Thanks to the people here http://blog.appliedinformaticsinc.com/how-to-parse-and-convert-json-to-csv-using-python/ for the actual csv.writer part.

