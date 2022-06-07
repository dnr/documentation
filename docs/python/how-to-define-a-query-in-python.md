---
id: how-to-define-a-query-in-python
title: How to define a Query in Python
sidebar_label: Define a Query
description: Define a Query
tags:
  - developer-guide
  - sdk
  - python
---

To define a Query, set the Query decorator [`@workflow.query`](https://python.temporal.io/temporalio.workflow.html#query) on the Query function inside your Workflow.

```python
@workflow.query
async def current_greeting(self) -> str:
    return self._current_greeting
```

The `@workflow.query` decorator defines a method as a Query. Queries can be asynchronous or synchronous methods and can be inherited; however, if a method is overridden, the override must also be decorated. Queries should return a value.

You can have a name parameter to customize the Queries' name, otherwise it defaults to the unqualified method name.
You can use `@workflow.Query(dynamic=True)`, which means all other unhandled Queries' fall through to this.

If `dynamic=True` is applied to your Queries' decorator, you can't have a `name` argument.
Your method parameters must be `self`, a string Query name, and a `*args` variable argument parameter.

For example:

```python
@workflow.query(dynamic=True)
def query_dynamic(self, name: str, *args: Any) -> str:
    return f"query_dynamic {name}: {args[0]}"
```

Queries should never mutate anything in a Workflow.