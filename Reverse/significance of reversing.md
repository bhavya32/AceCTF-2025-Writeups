# Read the reversed PNG file and restore it
with open("Reverseme.png", "rb") as f:
    data = f.read()

# Reverse the bytes
reversed_data = data[::-1]

# Write the restored PNG file
with open("Restored.png", "wb") as f:
    f.write(reversed_data)

print("File successfully restored as Restored.png")

Reverse the bytes. 

Then you see its not png through file cli. 

Execute it and get the flag.
