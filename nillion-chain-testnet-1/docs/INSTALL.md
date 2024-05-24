# Install

## Prerequisites

In addition to the node having the recommended [hardware](./SPECIFICATIONS.md) you will need the following on the node:

### Compile time dependencies
- Go 1.21+
- make and gcc

### Optional dependencies
- jq (useful for querying the fields from node statuses)

## Install binary

Clone and install nilliond:

```bash
git clone git@github.com:NillionNetwork/nilliond.git
cd nilliond
git checkout tags/v0.1.1
make install
```

Verify the binary:

```
nilliond version
```

should return v0.1.1
