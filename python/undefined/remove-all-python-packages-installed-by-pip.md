# Remove all Python packages installed by pip



### **Option 1:** 

Use below command –

```text
pip freeze | xargs pip uninstall -y
```

### **Option 2:**

If there are any packages which were installed usig VCS,  then we will exclude those . And then will remove the packages

```text
pip freeze | grep -v "^-e" | xargs pip uninstall -y
```

### **Option 3:**

* Get the list of all Python pip package in the requirements.txt file – Note: This OVERWRITES the Existing requirements.txt else will create new one.

```text
pip freeze > requirements.txt
```

* Remove all packages – one by one

```text
pip uninstall -r requirements.txt
```

* Remove all packages at once –

```text
pip uninstall -r requirements.txt -y
```

