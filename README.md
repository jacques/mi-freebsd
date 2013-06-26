# TextDrive FreeBSD Machine Image Builder

Originally forked from work I did to migrate my FreeBSD gateway box at
the TextDrive Cape Town office that does multiple PPPoE links to run
under KVM on SmartOS.

At TextDrive we built a FreeBSD 9.1-RELEASE-p3 KVM image for running
ontop of SmartOS in my spare time as a stop-gap to migrating legacy
FreeBSD Servers over to running inside zones on SmartOS for our
Shared Hosting product.

As part of the work building the template (we use a truck load of
Chef and custom compiled packages) as well as building in FreeBSD
specific bits.

The template built provides various bits and gets data from the
meta data API (either flat files on SmartOS or from
SmartDataCenter's Metadata API).

There are various patches from 3rd parties in the community which
we leverage to get a base image going.

## Meta Data Keys

<table>
  <tr>
    <th>Key</th>
    <th>Type</th>
    <th>Description</th>
    <th>Default</th>
  </tr>
  <tr>
    <td>builder</td>
    <td>boolean</td>
    <td>Whether we should not run finalisation scripts</td>
    <td>true</td>
  </tr>
</table>

## General Notes

 * The timezone is set to UTC
 * Root ssh logins are enabled for when using a ssh private key

## Post Install

### Switch out native drivers for virtio drivers

 * Download the latest drivers from http://people.freebsd.org/~kuriyama/virtio/

Requires work in the global zone to switch out the driver in the zone xml file.
