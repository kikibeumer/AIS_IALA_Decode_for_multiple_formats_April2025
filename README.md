This Jupyter notebook decodes encoded Automatic Identification System (AIS)
sentences into a human-readable, tabular data set. The resulting dataset is used
for interactive geospatial visualisation, but can be used for additional analysis
as well. The main script
1. reads a log file whose path you provide in file_path ;
2. determines whether each line is a proprietary timestamp sentence (e.g.
$PGHP) or a payload sentence (!AIVDM, !BSVDM, !AGVDM, . . . );
3. extracts or inherits the correct timestamp;
4. verifies the NMEA checksum with verify_checksum;
5. converts the six-bit ASCII payload to a binary string
6. and, following ITU R M.1371 bit layouts, decodes the desired fields (MMSI,
navigation status, ROT, SOG, longitude, latitude etc.).


Timestamp formats recognized
- ISO 8601 inline (2023-10-28T07:17:51.000Z) used in !BSVDM or !AIVDM
sentences.
- NMEA 0183 Talker time in the form dd-mm-yyyy hh:mm:ss (1459720797).
- Proprietary $PGHP format: $PGHP,1,yyyy,mm,dd,HH,MM,SS,sss,*hh.
- Tag-Block prefix (“\s:” or “\T:”) that carries a Unix epoch and/ or
human-readable stamp.
- Multi-fragment sentences where the timestamp is carried only in the
first fragment.
