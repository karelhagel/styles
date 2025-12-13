## With tight version control
### In @karelhagel/styles repo: bump version + tag

```
# in styles repo
npm version patch   # or minor/major (this updates package.json + creates a git tag)
git push --follow-tags
```


### In each client repo: pin dependency to a tag (most reliable)
In the client’s package.json:
```
"@karelhagel/styles": "github:karelhagel/styles#v0.1.2"
```
Then update when you release a new tag:
```
npm update @karelhagel/styles
```

## Without tight version control

### In @karelhagel/styles repo: bump version + tag

```
# in styles repo
npm version patch   # or minor/major (this updates package.json + creates a git tag)
git push --follow-tags
```


### In each client repo: pin dependency to a tag (most reliable)
In the client’s package.json:
```
"@karelhagel/styles": "github:karelhagel/styles"
```
Then update when you release a new tag:
```
npm update @karelhagel/styles
```
