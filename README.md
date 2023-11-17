# Silicon-rANS

This project is a single code sample showing one way to implement a
rANS decoder in Verilog. This decoder has the following properties:

- input is an unlimited length sequence of "fragments"
- each fragment is 2-3 bytes of header followed by a byte stream of rANS-compressed data
- stream output width is configurable
- the header contains the following information:
      - 1 bit to determine whether it's a 2 or 3 byte header
      - 1 bit to reset rANS state between fragments
      - 4 bits to select between 16 pre-baked probability distributions
      - 2 bits to temporarily narrow the width of the output stream for this fragment (allowing greater compression for regions where up to 3 msbs are never set)
      - either 8 or 16 bits to describe the length of the fragment

To meet timing, IO and compute are handled in alternating
cycles. Turning this into a solution where two decode threads are
operating concurrently using the same datapath is reasonably simple
but is left as an exercise for the reader.

The sample code refers to a "symbol vector assembly" which coordinates
the output of a group of these decoders and a "feeder" which
coordinates the input of a group of these decoders. The decoder can
operate without these so their implementation is also left as an
exercise for the reader.

The authors wish to thank Jarek Duda for creating the ANS family of
algorithms and Fabian Giesen for explaining them in a way that even
hardware engineers can understand.


## Contributing

This project is intended as a fairly static release of a piece of
sample code, so contributions/suggestions are not expected.

However, in the case that contributions are accepted, please note that
this project has adopted the [Microsoft Open Source Code of
Conduct](https://opensource.microsoft.com/codeofconduct/).  For more
information see the [Code of Conduct
FAQ](https://opensource.microsoft.com/codeofconduct/faq/) or contact
[opencode@microsoft.com](mailto:opencode@microsoft.com) with any
additional questions or comments.


## Trademarks

This project may contain trademarks or logos for projects, products,
or services. Authorized use of Microsoft trademarks or logos is
subject to and must follow [Microsoft's Trademark & Brand
Guidelines](https://www.microsoft.com/en-us/legal/intellectualproperty/trademarks/usage/general).
Use of Microsoft trademarks or logos in modified versions of this
project must not cause confusion or imply Microsoft sponsorship.  Any
use of third-party trademarks or logos are subject to those
third-party's policies.
