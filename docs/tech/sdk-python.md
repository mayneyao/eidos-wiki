---
sidebar_position: 3
---

# Eidos Python SDK

Python SDK for Eidos

## Install

```shell
pip install eidospy
```

## Usage

1. generate api endpoint from [eidos](https://eidos.space/settings/api). it should be like `https://api.eidos.space/rpc/ce52c92a-5c10-4acd-8638-ed0e5b19741e`
2. make sure API is enabled in the settings and Eidos client is open
3. initialize eidos client with the api endpoint

   ```python
   from eidospy import Eidos

   eidos = Eidos("__API_ENDPOINT__")
   ```

4. get space by name
   ```python
   space = eidos.space("eidos3")
   ```
5. manage resources in the space
   ```python
    table = space.table("532b30d66d984c8a9d9a0ef0245b0afb")
    doc = space.doc("532b30d66d984c8a9d9a0ef0245b0afb")
   ```

## Node

In Eidos, a Node is a universal concept that can represent a document, or a table. Each Node has a unique id, which can be used to retrieve the Node.

### create a node

```python
node = space.nodes.create(type="doc", title="", icon="")
print(node)

node = space.nodes.create(type="table", title="", icon="")
print(node)
```

### get node by id

```python
node = space.nodes.get("node_id")
print(node)
```

### query nodes

```python
nodes = space.nodes.query()
for node in nodes:
    print(node)
```

### update node

```python
space.nodes.update("node_id", {"title": "hello"})
```

### delete node

```python
space.nodes.delete("node_id")
```

## Table

### get row by id

```python
row = space.table("table_id").rows.get("row_id")
print(row)
```

### query rows

```python
rows = space.table("table_id").rows.query()
for row in rows:
    print(row)
```

### create row

```python
row = space.table("table_id").rows.create({"name": "hello"})
print(row)
```

### bulk create rows

```python
rows = space.table("table_id").rows.bulk_create([{"name": "hello"}, {"name": "world"}])
print(rows)
```

### update row

```python
space.table("table_id").rows.update("row_id", {"name": "hello"})
```

### delete row

```python
space.table("table_id").rows.delete("row_id")
```

## Doc

Eidos' documentation is implemented based on `lexical` and stored in a unique JSON format in the database to cater to the requirements of rich text formatting. Markdown is a more universally accepted documentation format, hence we have incorporated support for it. Eidos offers the capability to export documents, however, it's important to note that some information may be lost when rich text is exported as markdown.

Currently, the API only supports reading and writing in markdown and does not support rich text read/write operations.

<!-- ### get blocks

### append block -->

### create a new doc with markdown

```python
# 1. create a doc node
doc = space.nodes.create(type="doc", title="hello", icon="")
# 2. append markdown content
space.doc(doc["id"]).markdown.append("## hi")
```

### get markdown

```python
md = space.doc("doc_id").markdown.get()
print(md)
```

### append content with markdown

```python
space.doc("doc_id").markdown.append("## Hello")
```

the content will be appended to the end of the doc and transformed to Eidos Doc block content automatically.

## Sub-documents in Tables

In tables, each row can be expanded into a sub-document. Each row has its own `_id`, which is a UUID v4 string that includes hyphen characters, such as `f1b1b9b1-93e1-4b6e-8f4d-9b4f4b4b4b4b`.

When a record is expanded into a sub-document, the content of the sub-document is an independent document and a new document node is created. The ID of this node does not include hyphen characters, for example, `f1b1b9b193e14b6e8f4d9b4f4b4b4b4b`. The `parent_id` of this node is the ID of the original table node.
