from requests import get
import csv

#Inputs
start_yr = 2000
end_yr = 2014
input_file = 'Workbook1.csv'


tag = '<div class="info">'
#Open csv file with keywords in reader
inp = open(input_file,'rU')
reader = csv.reader(inp)

#Create a csv file to write results to
out_horz = open('NYTimes_Articles_horizontal.csv', 'wb')
writer_horz = csv.writer( out_horz )
header = ['keyword']
for i in range(start_yr, end_yr + 1):
    header.append( str(i) + ' count' )
writer_horz.writerow( header )

out_vert = open('NYTimes_Articles_vertical.csv', 'wb')
writer_vert = csv.writer( out_vert )
writer_vert.writerow( ['keyword', 'year', 'count'] )

#Loop through keywords
for row in reader:
    keyword = row[0]
    urlbase = 'http://chronicle.nytlabs.com/articles?keyword=' + keyword + '&year='
    horz_row = [keyword]
    #Loop through years
    for yr in range(start_yr, end_yr + 1):
        
        url = urlbase + str(yr) + '&offset=10'
        site = get(url)
        doc = site.text
        
        #Extract count
        ind = doc.find(tag)
        doc = doc[ind+len(tag):]
        ind1 = doc.find('of')
        ind2 = doc.find('article')
        doc = doc[ind1+2:ind2]    
        count = int(doc.strip())
        
        horz_row.append(count)
        #Write the review to csv
        writer_vert.writerow( [keyword, yr, count] )
    writer_horz.writerow( horz_row )
#Close csv
out_vert.close()
out_horz.close()
inp.close()
