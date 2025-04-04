---
title: "Try Except Finally"
date: 2025-04-04
---

Recently I was trying to debug a problem. We were iterating over a list of documents, processing them and sending upload requests to another server. If one of the upload requests fail, we delete already uploaded ones just to be atomic.

```python
exception_occurred = True
uploaded_docs = []
for doc in to_be_uploaded_docs:
  process(doc)
  try:
    upload(doc)
    uploaded_docs.append(doc)
  except CustomException:
    logger.info("ah shit here we go again")
    return
  else:
    exception_occurred = False
  finally:
    if exception_occurred:
      delete(uploaded_docs)

```

It is like above. After reading the code and I went to my team and said:

"Look guys, we don't delete the docs when CustomException occurs!!! I'm smart". 

They said. "Oh really, could you please handle that?". Yes of course said.

There was a problem though, luckily, that pushed me to the zone of learning... Some docs were being deleted, some were not.

But how come they can be deleted I asked to myself. Like... dude we **return** ... how come we can delete the docs...

I mean, apparently this is a feature of finally block. It is guaranteed to be executed even though "return" or "break" is called in the try, except and else blocks.

It simply amazed me. My ignorance is not an ending journey.
