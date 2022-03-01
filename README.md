# dendron-citations

tool for making dendron work well with citing things using bibtex or Zotero


# [`refs_vault_gen.py`](refs_vault_gen.py)

generates a vault of dendron notes corresponding to entries from a bibtex file


## Usage: 

```bash
python refs_vault_gen.py --bib_filename <bibtex_file> --vault_prefix <output_dir>
```
or simply
```bash
python refs_vault_gen.py <bibtex_file> <output_dir>
```

### Example:

for example, if the script and a bibtex file `refs.bib` are both located in the directory containing our `vault/`, we may write
```bash
python refs_vault_gen.py refs.bib vault/refs.
```

this will create notes of the form `refs.some-bibtex-key.md` in the `vault/` directory.



# Roadmap:

## bibtex integration
given a bibtex file, generate a vault of dendron notes bibtex keys as filenames

- add tags and other things from bibtex to metadata
- "beneath" each note for the bibtex, add another note for the citation itself.
	- note that this will all break if the bibtex keys change!
- this allows the user to reference the dendron notes instead of raw bibtex item
	- lets us use backlink features from dendron to see where something is cited

## zotero integration

do everything as for bibtex integration, but also:

- add links/copies in zotero to the dendron notes (when they exist)
- have zotero item materials inside dendron file
	- zotero notes, plaintext attachments inline
	- links to all other attachments
	- exclude the dendron file to avoid recursion, haha

## other

- to allow simpler references to papers, without having to type `[[dendron://refs-vault/<bibtex key>]]`, the user may create a vscode snippet in `> Preferences > Configure User Snippets > markdown.json`

```json
"dendron-cite": {
	"prefix": "@",
	"body": [
		"[[dendron://refs-vault/refs.$1]]"
	],
	"description": "dendron reference citation"
},
```

# dependencies:

- https://github.com/t-wissmann/biblib
	- needs to be installed manually, not on pypi
	- note: forked from https://github.com/aclements/biblib, which no longer works