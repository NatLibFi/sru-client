# SRU Javascript client library [![NPM Version](https://img.shields.io/npm/v/@natlibfi/sru-client.svg)](https://npmjs.org/package/@natlibfi/sru-client)

# Usage
## Retrieve all records
```js
import createClient from '@natlibfi/sru-client';
const client = createClient({url: 'https://foo.bar', recordSchema: 'marc'});

client.searchRetrieve('foo')
  .on('record', record => processRecord(string))
  .on('end', () => endProcessing())
  .on('error', err => handleError(err));
```
## Retrieve records only from the first response
```js
import createClient from '@natlibfi/sru-client';
const client = createClient({url: 'https://foo.bar', recordSchema: 'marc', retrieveAll: false});

client.searchRetrieve('foo')
  .on('record', record => processRecord(record))
  .on('end', nextRecordOffset => endProcessing(nextRecordOffset))
  .on('error', err => handleError(err));
```
# Configuration
## Client creation options
- **url**: The URL of the SRU service.
- **recordSchema**: Schema of the records. **Mandatory**.
- **version**: SRU version. Defaults to **2.0**.
- **maxRecordsPerRequest**: Maximum number of records to retrieve per requests. Defaults to **1000**.
- **recordFormat**: Format of the record argument in **record** event. Defaults to **string** (See export **recordFormats**)
- **retrieveAll**: Whether to retrieve all records or just from the first response. If **false**, the **end** event return the offset of the next record for the query
## searchRetrieve options:
The first parameter is the mandatory query string. Second is an optional object which supports the following properties:
- **startRecord**: The offset of the record from which to start fetching results from. See **retrieveAll** of the client creation options.
- **recordSchema**: Override default record schema
## License and copyright

Copyright (c) 2015, 2017-2018, 2020 **University Of Helsinki (The National Library Of Finland)**

This project's source code is licensed under the terms of **GNU Lesser General Public License Version 3** or any later version.
