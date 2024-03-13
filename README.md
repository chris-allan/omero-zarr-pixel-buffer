# OMERO Zarr Pixel Buffer

## Requirements

- OMERO 5.6+
- Java 11+

## Artifacts

The latest artifacts built and deployed by GitHub actions can be found on the
[Glencoe Software artifactory](https://artifacts.glencoesoftware.com/)

## Usage

The OMERO Zarr Pixel Buffer follows the principles of a classical OMERO.server
[service extension](https://omero.readthedocs.io/en/v5.6.10/developers/Server/ExtendingOmero.html#services).

After putting the `omero-zarr-pixel-buffer.jar` under `lib/server`, the server
must be restarted. To use the ZarrPixelBuffer, an Image or Mask object must be populated with
an [ExternalInfo](https://docs.openmicroscopy.org/omero-blitz/5.7.2/slice2html/omero/model/ExternalInfo.html)
object with the following properties:

-   `entityType` must be set to `com.glencoesoftware.ngff:multiscales`
-   `entityId` must be set to `3`
-   `lsid` must be set to the location of the Zarr data:
    - the absolute path to the dataset if available via the filesystem
    - an URI defined as `s3://s3.<region>.amazonaws.com/<bucket>/<path/to/dataset.zarr>`
      for datasets stored on Amazon  S3

Permissions for accessing Zarr dataset hosted on S3 buckets can be managed:

- either via named profiles stored under a local credentials file as for the AWS CLI
- or via EC2 instance profile condifigured with a policy allowing to assume an IAM role

## Development

Clone the repository:

    git clone https://github.com/glencoesoftware/omero-zarr-pixel-buffer

Run the Gradle build including the tests

    ./gradlew build

## License

The converter is distributed under the terms of the GPL license. Please see [LICENSE.txt](LICENSE.txt)
for further details.
