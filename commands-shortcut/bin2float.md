# binary file to float conversion

```python
import struct

f = open("./server_iq.dat", 'rb')
line = f.read()

for i in range(0,int(len(line)/4)):
    a = line[i*4:(i+1)*4]
    if i/2 == 0:
        i_data = struct.unpack('f', a)
        print(i_data)
    else:
        q_data = struct.unpack('f', a)
        print(q_data)

f.close()
```