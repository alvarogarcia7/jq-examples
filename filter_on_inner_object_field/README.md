2024-08-31 16:06:30 AGB

## Example of data

```json
"testGroups" : [
  {
    "curve" : "secp521r1",
    "encoding" : "asn",
    "type" : "EcdhTest",
    "tests" : [
      {
        "tcId" : 1,
        "comment" : "normal case",
        "public" : "30819b301006072a8648ce3d020106052b8104002303818600040064da3e94733db536a74a0d8a5cb2265a31c54a1da6529a198377fbd38575d9d79769ca2bdf2d4c972642926d444891a652e7f492337251adf1613cf3077999b5ce00e04ad19cf9fd4722b0c824c069f70c3c0e7ebc5288940dfa92422152ae4a4f79183ced375afb54db1409ddf338b85bb6dbfc5950163346bb63a90a70c5aba098f7",
        "private" : "01939982b529596ce77a94bc6efd03e92c21a849eb4f87b8f619d506efc9bb22e7c61640c90d598f795b64566dc6df43992ae34a1341d458574440a7371f611c7dcd",
        "shared" : "01f1e410f2c6262bce6879a3f46dfb7dd11d30eeee9ab49852102e1892201dd10f27266c2cf7cbccc7f6885099043dad80ff57f0df96acf283fb090de53df95f7d87",
        "result" : "valid",
        "flags" : []
        },
```

Source: https://github.com/C2SP/wycheproof/blob/master/testvectors/ecdh_secp521r1_test.json

## Distinct values of an internal field

Note: this is pseudo-language SQL:

```sql
SELECT distinct(result)
from testGroups[0].tests
from ecdh_secp521r1_test.json
```

```bash
cat ecdh_secp521r1_test.json | jq -r '.testGroups[0].tests[] | .result' | sort | uniq -c
 229 acceptable
  55 invalid
 208 valid
```

## Filter by an internal field

```sql
SELECT distinct(length(t.public))
from testGroups[0].tests t
from ecdh_secp521r1_test.json
where t.result == "invalid"
```

```bash
cat ecdh_secp521r1_test.json | jq -r '.testGroups[0].tests[] | select (.result=="invalid") | .public | length' | sort | uniq -c
   1 1042
   5 1172
   3 160
   2 168
   2 176
  11 180
   2 182
   2 184
   1 186
   2 216
   1 240
   2 248
  20 316
   1 46
```

Note: `ecdh_secp521r1_test.json` is https://github.com/C2SP/wycheproof/blob/master/testvectors/ecdh_secp521r1_test.json
