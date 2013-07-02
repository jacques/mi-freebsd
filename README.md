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
 * Using DHCPd on the network interfaces -- update /etc/rc.conf to do static IP
   instead (DHCP on kvm is a bit broken -- the interface sometimes reports as
   being up but does not receive the dhcpd server response).

## Post Install

### Switch out native drivers for virtio drivers

 * Download the latest drivers from http://people.freebsd.org/~kuriyama/virtio/

Requires work in the global zone to switch out the driver in the zone xml file.

## License

```
Copyright (c) 2013 Jacques Marneweck.  All rights reserved.
Copyright (c) 2013 Text Industries, Llc. All rights reserved.

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE
```
