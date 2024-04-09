# setup-quantum-cli

A small Github Action to setup [quantum-cli](https://cli.planetary-quantum.com).

```yaml
- uses: hostwithquantum/setup-quantum-cli@main
  with:
    username: ${{ secrets.QUANTUM_USERNAME }}
    password: ${{ secrets.QUANTUM_PASSWORD }}
- run: quantum-cli validate
```
