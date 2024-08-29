# Dynamic batching

```py
import time, random
from batching import BatchProcessor

def fake_predict(X: list):
    # model accepts a batched input (or list here)

    time.sleep(4)
    n = len(X)
    return [random.choice([0, 1]) for _ in range(n)]

# Create a batch processor for our prediction function with max batch size of 16 and batch timeout of 1 second
batch_processor = BatchProcessor(fake_predict, bs=16, timeout=1)
```


`batch_processor.process` puts the input into a queue and returns a future object that can be used to get the result when it's ready.
```py
# batch_processor.process is non-blocking
input = 1
future = batch_processor.process(input)
print(future)
```

