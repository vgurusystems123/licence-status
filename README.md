# licence-status

Online licence status for the Smart products (SmartCompliance, SmartAttendance, …).

Each licence has one file, `<product>/<licence-id>.txt`. It holds the licence ID, the product, whether the licence is
revoked, and a timestamp, signed with the vendor's key. Installed apps read their own file from
`https://raw.githubusercontent.com/vgurusystems123/licence-status/main/<product>/<licence-id>.txt` every few hours.
They check the signature, refuse a file that belongs to another licence or is older than one already seen, and lock
if they can't read it for several days.

The repository is public on purpose, so customer servers need no credentials. It contains no customer names, and the
files can't be forged or edited without the vendor's private key.

The files are managed only with the licence tool (smart-licence-kit `tools/licence-tool`), never by hand:

    java LicenceTool.java issue     … --status-dir <this checkout>
    java LicenceTool.java revoke    --key … --product <p> --licence-id <id> --status-dir <this checkout>
    java LicenceTool.java reinstate --key … --product <p> --licence-id <id> --status-dir <this checkout>
