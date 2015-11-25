README
======

Replay SOLR queries parsed from nginx logs.

Usage
-----

Use `-addr` to point to a SOLR to warm up. Use `-run` flag to actually run the queries.

    $ zcat log-20151124.gz | ripley -addr 10.10.110.7:8085 -run
    {"elapsed":0.270542267,"status":"200 OK","url":"http://172..."}
    {"elapsed":0.287049684,"status":"200 OK","url":"http://172..."}
    ...

Run queries in parallel with `-w` parameter:

    $ zcat log-20151124.gz | ripley -addr 10.10.110.7:8085 -w 8 -run
    {"elapsed":0.270542267,"status":"200 OK","url":"http://172..."}
    {"elapsed":0.287049684,"status":"200 OK","url":"http://172..."}
    ...

To get timing information out (in seconds), use [jq](https://stedolan.github.io/jq/):

    $ zcat log-20151124.gz | ripley -addr 10.10.110.7:8085 -run | jq -r '.elapsed'
    0.26466516700000003
    0.22494069300000002
    6.027045224
    6.151381966
    0.24651203600000002
    0.23020700700000002
    0.24007809400000002
    0.240172403
    0.24043798600000002
    0.240256606
    ...
