# prerequisites:  
# a file in working directory containing the results of your ldapsearch (see readme).  Here it's called ldapresults.txt
# an empty csv in working directory. Here it's called uniqdata.csv.

import re
import csv
import json

infile = open('ldapresults.txt')
contents = infile.read()
infile.close()

nocommas = contents.replace(',',';')
ndnewlines = nocommas.replace('\n\n','}')
startbrack = ndnewlines.replace('dn:','{dn:')
addcommas = startbrack.replace('\n',',')
jswrap = '{\"umichpeople\": [' + addcommas + ']}'

yikes = re.sub(r'(\w+)(?=:)',r'"\1"',jswrap,flags=re.M)
likes = re.sub(r': (\w[^,}]+)(,|})',r': "\1"\2',yikes,flags=re.M)

jparsed = json.loads(likes)
# print jparsed

nifty_data = jparsed["umichpeople"]
print nifty_data

# open a file for writing

uniqdata = open('uniqdata.csv', 'w')

# create the csv writer object

csvwriter = csv.writer(uniqdata)

count = 0

for emp in nifty_data:

      if count == 0:

             header = emp.keys()

             csvwriter.writerow(header)

             count += 1

      csvwriter.writerow(emp.values())

uniqdata.close()
