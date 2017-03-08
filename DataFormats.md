Processing XML in Hadoop:

	Hadoop Input Formats
		Hadoop input formats is made of two principal components
			1. Logical Splits and Not Physical Splits
			2. Record Readers to read records from individual split
		Each splitted chunk is sent to individual Mappers for processing. However, Splits form the rough boundary of the data to be processed by an individual Mapper. The FileInputFormat (and it’s subclasses) generate splits on overall file size. 
		Of course, it’s unlikely that all individual Records (a Key and Value that are passed to each Map invocation) lie neatly within these splits: records will often cross splits. 
		The RecordReader, therefore, must handle this, on whom, lies the responsibilty to respect record-boundaries and present a record-oriented view of the logical InputSplit to the individual task.
		In short, a RecordReader could scan from the start of a split for the start of it’s record. It may then continue to read past the end of it’s split to find the end. 
		The InputSplit only contains details about the offsets from the underlying file: data is still accessed through the streams.
For anyone trying to process XML with Hadoop: try Mahout’s XmlInputFormat.
