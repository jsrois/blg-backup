# Using Python Threads to monitor a SMB connection -based download



### The problem

```python
    def download(self, dataset_name, local_file):
        self.connect()
        matches = self.find_dataset_matches(dataset_name)
        if not matches:
            raise NonExistentRemoteDataset(dataset_name)
        remote_dataset = matches[0]
        remote_dataset_size = remote_dataset.file_size
        print "Downloading {} bytes".format(remote_dataset_size)
        with open(local_file, 'wb') as fp:
            self.connection.retrieveFile(self.SERVICE,
                                         "{}/{}.rar".format(self.PATH, dataset_name),
                                         fp)
            // < we could use some feedback here
        self.connection.close()
```