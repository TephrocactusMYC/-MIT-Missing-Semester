# Git’s data model
## Snapshots
Git models the history of a collection of files and folders within some top-level directory as a series of snapshots. In Git terminology, a file is called a “blob”, and it’s just a bunch of bytes. A directory is called a “tree”, and it maps names to blobs or trees (so directories can contain other directories).

example:
```shell
<root> (tree)
|
+- foo (tree)
|  |
|  + bar.txt (blob, contents = "hello world")
|
+- baz.txt (blob, contents = "git is wonderful")
```
## Modeling history: relating snapshots
In Git, a history is a directed acyclic graph (DAG) of snapshots.

## Data model, as pseudocode
```C
// a file is a bunch of bytes
type blob = array<byte>

// a directory contains named files and directories
type tree = map<string, tree | blob>

// a commit has parents, metadata, and the top-level tree
type commit = struct {
    parents: array<commit>
    author: string
    message: string
    snapshot: tree
}
```
## Objects and content-addressing
An “object” is a blob, tree, or commit:
```C
type object = blob | tree | commit
```
In Git data store, all objects are content-addressed by their SHA-1 hash.
```python
objects = map<string, object>

def store(object):
    id = sha1(object)
    objects[id] = object

def load(id):
    return objects[id]
```

## References
Git uses references, which are human-readable names assigned to the SHA-1 hash values of snapshots, as pointers to commits. These references can be updated and typically point to the latest commit on a branch, such as the master reference pointing to the latest commit on the main branch.
```python
references = map<string, string>

def update_reference(name, id):
    references[name] = id

def read_reference(name):
    return references[name]

def load_reference(name_or_id):
    if name_or_id in references:
        return load(references[name_or_id])
    else:
        return load(name_or_id)
```
**Git uses a special reference called "HEAD" to indicate the current position in history.**

## Staging area
Git uses a "staging area" to specify which modifications should be included in the next snapshot, allowing for clean snapshots and accommodating scenarios where specific changes need to be committed.

## Command line api
All things for this section are written [here](../more%20information/Pro-Git.md).




