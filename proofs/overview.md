Updated table variant (different from thesis): Considered new optimizations and model changes in proofs

- Goal: minimize number of required manual interactions

| Type | Model    | Assumption Details         | Interaction | Verif. | Time (s) | # Steps | Helper Lemmas |
|------|----------|---------------------------|-------------|--------|----------|---------|---------------|
| san. | PKI      |                           | ---         | ✔      |          |         |               |
|      | CT       |                           | ---         | ✔      |          |         |               |
|      | Audit    |                           | ---         | ✔      |          |         |               |
|      | Gossip   |                           | ---         | ✔      |          |         |               |
| T    | CT       | w/o MMD                   | manual      | ✗      |          |         |               |
|      |          | with MMD                  | manual      | ✗      |          |         |               |
|      |          | honest logger             | ---         | ✔      |          |         |               |
|      | Audit    |                           | ---         | ✔      |          |         |               |
|      | Gossip   | w/o client proof          | manual      | ✗      |          |         |               |
|      |          | with client proof         | manual      | ✗      |          |         |               |
| AT   | CT       | clientside                | SUFF        | ✔      |          |         |               |
|      |          | monitor with client       | ---         | ✔      |          |         |               |
|      |          | monitor alone             | ---         | ✗      |          |         |               |
|      | Audit    |                           | ---         | ✔      |          |         |               |
|      | Gossip   |                           | SUFF        | ✔      |          |         |               |
| AA   | PKI Ext. | external validator        | ---         | ✔      |          |         |               |
|      | CT Ext.  | monitor validator         | ---         | ✔      |          |         |               |
|      |          | client blames log         | SUFF(min2)  | ✔      |          |         |               |
|      |          | monitor blames log        | SUFF(min2)  | ✔      |          |         |               |
|      | CT       | monitor fetches log       | NONEMP      | ✗      |          |         | uniq takes    |
|      |          | m. fetches benign log     | ---         | ✔      |          |         |               |
|      | Audit    |                           | ---         | ✔      |          |         |               |
|      |          | added logger blame        | SUFF(min2)  | ✔      |          |         |               |
|      | Gossip   |                           | SINGLE,EMP  | ✗      |          |         | uniq needshelp|
|Revoc.| CT       | perfect transparency      | ---         | ✔      |          |         |               |
|      |          | cond. transparency        | ---         | ✔      |          |         | MIN           |
|      |          | non-guaranteed transp.    | ---         | ✗      |          |         | MIN+UNIQ      |
|      | Audit    |                           | ---         | ✔      |          |         | MIN           |
|      | Gossip   |  ???                      |             | ✔      |          |         |               |
