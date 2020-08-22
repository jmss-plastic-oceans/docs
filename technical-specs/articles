# Articles

## How are articles read by the website?
1. Website has a Google Sheet export url embedded in the Javascript (manually put there)
    - This URL is set to export the sheet as CSV (comma-seperated)
2. Website launches a fetch request towards the Google Sheet and recieves the CSV file.
    1. Google recently put a CORS header on their servers which means we can't query the URL directly. So, I have setup a CORS reverse proxy to strip these headers. [Here is the source code of the service I am using](https://github.com/Rob--W/cors-anywhere). It is hosted on Heroku at the URL [https://srg-cors-proxy.herokuapp.com](https://srg-cors-proxy.herokuapp.com)
    2. The URL for this CORS proxy is embedded in the program.
    3. The fetch request is launched through the CORS proxy.
3. Website gets this information and perform preliminary parsing.
    1. First, we need to parse the actual .CSV file. The reason I chose CSV is because it was an easy format to parse by text.
    2. We split by lines, then by commas. This will give as a array-of-arrays of the entire sheet. (This is also the reason we can't have commas in the title or description - the program will recognise it as another column)
4. The website now has the title, description, and image URLs. But it does not have the body. This is contained in a seperate Google Doc, which we also have to fetch
    1. We get the document ID by using a bit of regex and make a URL that will export it to .TXT
    2. We make a fetch request though the same CORS proxy.
5. The website now has the title, description and body. We create elements for each article using `document.createElement()` and nest them within each other. Then, we append it to the website.

Done.
