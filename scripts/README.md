## Batch deposit helper script

Use this script to send multiple SBC deposits in batches.

First, make sure you have generated valid deposits via a deposit cli (https://github.com/openethereum/sbc-deposit-cli).
You will need a `deposit_data.json` file from there.

Now, copy `./scripts/.env.example` file to `./scripts/.env` and update necessary parameters.

Then run the following:
```bash
docker build -f ./scripts/Dockerfile -t batch_deposit .

# docker run --env-file ./scripts/.env -v /path/to/deposit_data.json:/tmp/deposit_data.json batch_deposit /tmp/deposit_data.json

# removed entrypoint in Dockerfile so use blo stead
docker run --env-file ./scripts/.env -v /path/to/deposit_data.json:/tmp/deposit_data.json batch_deposit node scripts/deposit.js /tmp/deposit_data.json
# o
docker run -it --env-file ./scripts/.env -v /path/to/deposit_data.json:/tmp/deposit_data.json batch_deposit bash
root@870cc7bfe9f8:/app# node scripts/deposit.js /tmp/deposit_data.json
```

This will read the `deposit_data.json` file and submit deposits from `OFFSET` to `OFFSET + N - 1` to the deposit contract.
