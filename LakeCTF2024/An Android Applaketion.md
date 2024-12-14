- **Challenge description**: just an Android reg challenge
- **Challenge category**: Rev
- **Challenge points**: 170

Another z3 challenge, how original.


### Solution

We are given an APK file, which is an android application file.
Luckily, we have jadx, a tool for reverse-engineering.

When opening it we see a lot of functions that have been renamed.
```
/* renamed from: EPFL02be4ef455aecf9f0e31ed402aeb291ad9691c544c79074a0cc95c220914ac4d */ public native boolean m13x45c1db7d(String str); /* renamed from: EPFL03b3c5910835e3b842838cbbcf18d7132aaaca480c70df128a0dbe04f6c85367 */ public native boolean m14x67a4aa48(String str); /* renamed from: EPFL03b42a6a21cd00661e7d18200cc7419c66652c26b2fbfdc782830d34225fd118 */ public native boolean m15x1593b3f5(String str); /* renamed from: EPFL04186174198c6b539e23815906331ddd133f0f0206de1da15585d65fdd61e925 */ public native boolean m16xc21cbd9d(String str); /* renamed from: EPFL05747afdf2a4fd4f5ac97bad92f26f6b06913e8a53e00d245a4099b12777cd3f */ public native boolean m17xf1209ea3(String str); /* renamed from: EPFL06834c0a7262bc9a8e9972b1182d79050af908322d23d6b428ce106bc6e79c8c */ public native boolean m18xa613f238(String str); /* renamed from: EPFL07acb0506422a548dd34422a5f43e2d6137ccb764b45579f3ed0681c2eb1f16f */ public native boolean m19x6a799c4f(String str); /* renamed from: EPFL08b64ee2894508fe3b0cdad5fb82eee8dcb152ee5f86ec36a96a1096c5851e5e */ public native boolean m20x8b57389a(String str); /* renamed from: EPFL08d9ac0630e7a1f5164a4903e53786c03dcf6b46b3260766e38ecaa5fe3ed4a0 */ public native boolean m21xa39b3198(String str); /* renamed from: EPFL091f7758acb778d09affe341a5af54bc4bdfe955b344e471de6780d1b9cc4756 */ public native boolean m22xbd54d6a2(String str); /* renamed from: EPFL09c88b614e9deba897896426268053236863ac2e1c535785a218e4a0f3ea0a6c */ public native boolean m23xd75f1840(String str); /* renamed from: EPFL0a477f2413e4c0e4cdbbdf5f49383ce77c674d5aa3c38d44c1dd74d1b74afc6d */ public native boolean m24x4cd6741f(String str); /* renamed from: EPFL0a7e79b0395125d73dcbdafa7e9ce71b892c24fb8e97ef4998eaa0c31b34c5ad */ public native boolean m25xb22ee4fd(String str); /* renamed from: EPFL0a8bdc8a2283dcd5cceb7dc6ac6122157b6e561f4a590d3d2d51c1acb02cce28 */ public native boolean m26xd7444808(String str); /* renamed from: EPFL0af97955f73a524bb84174cadd935403df823027a4fb2c1b06ee9f105f94f31e */ public native boolean m27xfa182999(String str);
```

And a big if statement at the end.

```
if (m283xc838c637(obj) && m182x7693666a(obj) && m195x62599589(obj) && m278xed90ff5(obj) && m165x435304e4(obj) && m222x6826a71f(obj) && m544xffd8abd0(obj) && m571xff8b8d62(obj) && m449x5294c2c7(obj) && m515xa6e4c941(obj) && m276x90d0f8d2(obj) && m534x9c8c74b0(obj) && m592xfa6a8b14(obj) && m245xc4ed51ca(obj) && m289x427f2026(obj) && m103xb0ab96e1(obj) && m151x8b5857ca(obj) && m465x7481322e(obj) && m161x8f4df15c(obj) && m467x53f75ba3(obj) && m433x9a903520(obj) && m371x42f280d3(obj) && m413xf267ae8f(obj) && m366x6408d1bf(obj) && m480x712e07cc(obj) && m25xb22ee4fd(obj) && m455x7f5a8309(obj) && m42x444da669(obj) && m337x9636ac69(obj) && m237x1061a1e9(obj) && m520x4d615744(obj) && m596xcaefe32(obj) && m311x802b4867(obj) && m226x245ee57f(obj) && m448x7823caf1(obj) && m391x5e7b31c0(obj) && m559xf30588b0(obj) && m600x9283d759(obj) && m339x3273289d(obj) && m503xb2d14f66(obj) && m350x8dbc7637(obj) && m374x8bc309d6(obj) && m432xdd2edaf6(obj) && m324xdd880965(obj) && m379x7fb9eb48(obj) && m192xd34a723f(obj) && m582xb792e228(obj) && m502x1d1dd6e9(obj) && m128xc52797dd(obj) && m224xa0087ea9(obj) && m409x59850d68(obj) && m440xeb72e784(obj) && m268xb59560c4(obj) && m172xaa0d4d81(obj) && m211x3e665fa(obj) && m88xe6a1798d(obj) && m333xa87dffd(obj) && m564xa55081ad(obj) && m36x974e61c9(obj) && m308xfa3abee6(obj) && m485xc80e446b(obj) && m506xacdbedbb(obj) && m484xf8b1b9b0(obj) && m517xc315e15c(obj) && m52x1e916fba(obj) && m38x7967acee(obj) && m567xbc31575e(obj) && m186x3105636(obj) && m219x7495a216(obj) && m357xa87efee1(obj) && m539xdf2083fa(obj) && m470xeaab01bc(obj) && m21xa39b3198(obj) && m56xad22a33d(obj) && m349x14c0b776(obj) && m312x99087a1d(obj) && m318xc973e82e(obj) && m331xf0224bb8(obj) && m325xfc8bf395(obj) && m451x710491f5(obj)) {

textView.setText("flag is correct!");

} else {

textView.setText("flag is wrong...");

}

}
```

If there are renaming, it means the functions must be imported from somewhere.

an APK file is essentially a zip file, so we can unzip it to find `libohgreat.so` in /lib
and inside, using ida, we can find the functions.

Luckily, IDA has a nice feature called python scripts, so using ida and the big decompiled java file we start to work!

```python
import re

# Read the input file
with open('big.java', 'r') as file:
    input_text = file.read()

# Adjusted regex pattern for multi-line comments and function definitions
pattern = re.compile(
    r'/\*\s*\* renamed from:\s*\* (EPFL[0-9a-f]+)\s*\*/\s*public native boolean (\w+)\(String str\);',
    re.MULTILINE
)

# Find matches
matches = pattern.findall(input_text)

# Create a dictionary from the matches
result = {match[0]: match[1] for match in matches}

with open("namedict.txt", "w") as file:
    for key, value in result.items():
        file.write(f"{key}:{value}\n")
```

And from ida:

```python
import re

# Read the input file
with open('big.java', 'r') as file:
    input_text = file.read()

# Print the input for debugging
print(input_text)

# Adjusted regex pattern
pattern = re.compile(
    r'/\* renamed from: (EPFL[0-9a-f]+) \*/\s+public native boolean (\w+)\(String str\);'
)

# Find matches
matches = pattern.findall(input_text)

# Create a dictionary from the matches
result = {match[0]: match[1] for match in matches}

# Print the result
print(result)

```

And then after a big of filtering, we get to the z3!

```python


from z3 import BitVec, Solver, sat
v3 = [BitVec("b_{:02d}".format(i), 8) for i in range(63)]


solver = Solver()
for i in range(63):
    solver.add(v3[i] > 0x20)
    solver.add(v3[i] <= 0x7f)


prefix = "EPFL{"
suffix = "}"
for i, char in enumerate(prefix):
    solver.add(v3[i] == ord(char))
solver.add(v3[62] == ord(suffix))


for i in range(63):
    solver.add(v3[i] >= 32, v3[i] <= 126)


# Add the provided constraints
constraints = ['(v3[17] ^ (v3[4] ^ v3[47])) == 111', 'v3[14] - (v3[17] + v3[35]) == -195', '(v3[11] ^ (v3[62] ^ v3[23])) == 125', 'v3[24] + v3[37] + v3[6] == 149', 'v3[23] + v3[20] + v3[54] == 364', 'v3[28] - (v3[17] + v3[0]) == 43', 'v3[31] - (v3[8] + v3[42]) == -175', 'v3[0] + v3[53] + v3[28] == 189', 'v3[48] - (v3[14] + v3[61]) == -75', 'v3[59] + v3[57] + v3[61] == 265', 'v3[25] - (v3[54] + v3[13]) == -120', '(v3[19] ^ (v3[32] ^ v3[9])) == 91', 'v3[11] + v3[53] + v3[8] == 319', '(v3[31] ^ (v3[54] ^ v3[50])) == 111', 'v3[54] + v3[45] + v3[43] == 315', '(v3[43] ^ (v3[45] ^ v3[4])) == 122', 'v3[36] - (v3[25] + v3[17]) == -205', 'v3[46] - (v3[56] + v3[13]) == 60', 'v3[61] - (v3[9] + v3[48]) == -74', 'v3[9] + v3[45] + v3[24] == 181', 'v3[13] + v3[7] + v3[45] == 307', '(v3[48] ^ (v3[52] ^ v3[36])) == 84', 'v3[24] - (v3[58] + v3[16]) == -62', 'v3[7] - (v3[50] + v3[62]) == -98', 'v3[46] + v3[33] + v3[56] == 220', '(v3[5] ^ (v3[3] ^ v3[12])) == 116', '(v3[30] ^ (v3[53] ^ v3[12])) == 35', '(v3[56] ^ (v3[48] ^ v3[9])) == 57', 'v3[50] - (v3[40] + v3[57]) == 2', '(v3[6] ^ (v3[5] ^ v3[47])) == 65', '(v3[20] ^ (v3[41] ^ v3[16])) == 74', '(v3[8] ^ (v3[6] ^ v3[12])) == 32', '(v3[11] ^ (v3[41] ^ v3[16])) == 119', 'v3[31] + v3[62] + v3[19] == 136', 'v3[48] + v3[25] + v3[45] == 191', 'v3[37] - (v3[43] + v3[23]) == -133', 'v3[58] - (v3[17] + v3[0]) == -218', 'v3[58] - (v3[56] + v3[53]) == -135', 'v3[24] + v3[40] + v3[35] == 265', '(v3[2] ^ (v3[11] ^ v3[24])) == 86',
               '(v3[7] ^ (v3[6] ^ v3[39])) == 95', 'v3[47] + v3[42] + v3[52] == 99', 'v3[26] - (v3[33] + v3[24]) == -172', 'v3[27] + v3[4] + v3[57] == 185', 'v3[29] + v3[51] + v3[50] == 252', 'v3[5] + v3[35] + v3[52] == 202', 'v3[0] - (v3[1] + v3[12]) == 27', '(v3[22] ^ (v3[4] ^ v3[56])) == 81', 'v3[26] + v3[61] + v3[19] == 181', 'v3[32] + v3[14] + v3[30] == 130', 'v3[18] + v3[30] + v3[42] == 99', 'v3[47] + v3[32] + v3[45] == 160', 'v3[34] + v3[21] + v3[44] == 310', '(v3[26] ^ (v3[31] ^ v3[23])) == 71', 'v3[16] + v3[15] + v3[2] == 172', '(v3[50] ^ (v3[25] ^ v3[48])) == 80', 'v3[44] - (v3[34] + v3[40]) == -80', '(v3[57] ^ (v3[54] ^ v3[29])) == 105', '(v3[22] ^ (v3[55] ^ v3[36])) == 70', '(v3[54] ^ (v3[21] ^ v3[11])) == 57', 'v3[20] + v3[26] + v3[60] == 367', 'v3[32] + v3[24] + v3[7] == 132', '(v3[38] ^ (v3[34] ^ v3[25])) == 83', 'v3[31] - (v3[38] + v3[14]) == -162', '(v3[39] ^ (v3[3] ^ v3[44])) == 74', 'v3[57] - (v3[8] + v3[3]) == -46', 'v3[4] + v3[40] + v3[5] == 246', 'v3[51] + v3[32] + v3[26] == 350', 'v3[9] - (v3[5] + v3[18]) == -213', 'v3[19] + v3[34] + v3[45] == 224', 'v3[52] + v3[9] + v3[48] == 363', 'v3[28] + v3[15] + v3[61] == 347', 'v3[51] - (v3[46] + v3[13]) == 15', 'v3[4] - (v3[42] + v3[45]) == -53', 'v3[26] + v3[25] + v3[12] == 158', '(v3[22] ^ (v3[5] ^ v3[57])) == 102', 'v3[7] - (v3[28] + v3[43]) == -174', 'v3[8] - (v3[1] + v3[12]) == 22', 'v3[5] - (v3[25] + v3[47]) == -43', 'v3[47] - (v3[5] + v3[61]) == -144']
print(len(constraints))
for constraint in constraints:
    solver.add(eval(constraint))


# Check satisfiability
if solver.check() == sat:
    model = solver.model()
    # Reconstruct the string
    result = ''.join(chr(model[v3[i]].as_long()) for i in range(63))
    print(f"Solved string: {result}")
else:
    print("No solution found!")
```

And we got our flag!