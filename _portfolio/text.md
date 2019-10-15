---
layout: post
title: Text for C++
feature-img: "assets/img/pexels/adult-art-asia-engin-akyurt.jpg"
img: "assets/img/pexels/adult-art-asia-engin-akyurt.jpg"
date: October 15th, 2019
tags: [C++, Unicode, Text, 🚌, ⌨️]
---


There does not exist a good, flexible, backwards-compatible solution for Text in C++. Choosing a library either requires taking the entire thing (Qt), getting involved in a very complex interface (ICU), dealing with sometimes limiting API choices (CopperSpice), or having a well-done but very opinionated design set (the proposed Boost.Text).

Where is the standard library-friendly, maximum performance solution for handling text encoding and decoding in C++ and C?

This project is the push to reach that goal.




# Current Funding

The project has the goal of being fully funded by mid 2020 so that all users can have a high quality solution of text that is not kept within one company or ecosystem, but ported to the Standard Library for use by everyone. Work hours are laid out [in this proposal here](https://github.com/ThePhD/text/blob/develop/docs/funding/2019.09.21%20-%20Towards%20Text%20in%20the%20Standard%20Library%20-%20ThePhD.pdf).

Funding goes toward:

- Funding development;
- Targeting specific features;
- Covering general library support;
- Covering specific company or vendor support;
- and, Attending WG14 (C Committee) and WG21 (C++ Committee) meetings.


Specialized solutions for C++11 (or C++03) can be made. If you, your company or organization is interested in helping or need special features/early access to features listed below, please [contact me](phdofthehouse@gmail.com).



## Funding Goals and Progress

Below are the published funding goals. Sponsors may pay into specific goals or, if given a large enough donation, create a new goal entirely; otherwise, funding falls into the categories in a top-to-bottom, linear fashion. Goals marked (_Stretch_) are not quite bare-minimum necessary, but would be absolutely wonderful to accomplish!

_Current Goal: Get to Full Time Development_

$505 USD / $82,000 USD

[ ⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀ ]




# Technical Details

The work is ongoing in these repositories here:

- [C++](https://github.com/ThePhD/text);
- and, [C](https://github.com/ThePhD/cuneicode).

The C++ library submodules and builds on top of the C one for fast-path functions. Internally, the C library is implemented with C++ and -- hopefully soon in the future -- vectorization by hand or with [SIMD/`std::experimental::simd`](https://en.cppreference.com/w/cpp/experimental/simd/simd). The principals and inner workings of the implementation are detailed in a series of talks, slides and posts:

- Catching ⬆️ - The (Baseline) Unicode Plan for C++23 - ThePhD; Friday, September 20th, 2018; CppCon 2019; Aurora, Colorado
  - [Video](https://www.youtube.com/watch?v=BdUipluIf1E)
  - [Slides](docs/presentations/2019.09.20%20-%20Catching%20⬆️%20-%20The%20(Baseline)%20Unicode%20Plan%20for%20C++23%20-%20ThePhD%20-%20CppCon%202019.pdf)
  - [Comments](https://www.reddit.com/r/cpp/comments/de1jy9/cppcon_2019_jeanheyd_meneide_catch_unicode_for_c23/)
  - [Abstract](https://cppcon2019.sched.com/event/7823aebeede8d50e1daa70b5c22ab0a4)
- A Rudimentary Unicode Abstraction - ThePhD; Wednesday, March 7th, 2018; Study Group 16; Boston, Massachusetts
  - [Slides](docs/presentations/2018.03.07%20-%20a%20rudimentary%20unicode%20abstraction%20-%20ThePhD%20-%20SG16%202018.pdf)

The current spread of goals is as follows.


### Ⅰ: Core Text Utilities [ 2% ] 

- Encoding objects for one-by-one encoding and decoding.
  - `utf8`, `utf16`, `utf32`, `narrow_execution` and `wide_execution` Encoding Object types;
  - and, `basic_utf8<char_type>`, `basic_utf16<char_type>`, and `basic_utf32<char_type>` types.
- `decode(...)`, `encode(...)`, and `transcode(...)` functions.
- `decode_view<encoding, ...>`, `encode_view<encoding, ...>`, and `transcode_view<encoding, ...>` range types.

[ ⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀ ]


### Ⅱ: Normalization Forms [ 0% ]

- All four Unicode Normalization Forms, as specified in [UAX #15](https://unicode.org/reports/tr15/).
  - Canonical Form `nfc`
  - Canonical Form `nfd`
  - Compatibility Form `nfkc`
  - Compatibility Form `nfkd`
- `text_view<Encoding, NormalizationForm, Container>`
- `text<Encoding, NormalizationForm, Container>`

[ ⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀ ]


### Ⅲ: User Extensibility Hooks for (User) Encodings [ 0% ]

- `text_encode`, `text_decode`, `text_transcode`, and `text_transcode_one` free function ADL hooks

[ ⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀ ]


### Ⅳ: Byte Buffers and Streaming [ 0% ]  

- `encoding_scheme<Encoding, endian, Byte>` - transformative encoding that always presents its code unit type as `Byte` (defaults to `std::byte`).
- `incomplete_handler<Handler>` - finish incomplete sequences and execute underlying handler if sequence is incomplete.

[ ⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀ ]


### Ⅴ: CJK Encoding Tests [ 0% ]

- Implement `gb18030`, the official government Unicode Transformation Format encoding of PRC.
- Implement legacy `shift_jis`/`euc_jp`/`iso2022_jp` legacy encodings.
  - priority goes to `shift_jis`/`euc_jp` as it encodes more traffic.

[ ⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀ ]


### Ⅵ: (_Stretch_) Enhanced Execution Encoding [ 0% ]

- Reach into platform-specific functions to rip out guts of platform's current encoding to ensure preservation of Unicode in:
  - `narrow_execution`
  - `wide_execution`

[ ⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀ ]


### Ⅶ: (_Stretch_) Hyper-Scrutinized Vectorization Implementation [ 0% ]

- Apply vectorization techniques for conversions to pairs of encodings in `ascii`, `utf8`, `utf16`, and `utf32`.

[ ⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀ ]


### Ⅷ: (_Stretch_) C Library for Span-Based Conversions [ 0% ]

- As detailed in proposal [N2440](/vendor/future_cxx/papers/source/C - Efficient Character Conversions.html): C functions for fast conversions.
- Take functionality through all of WG14, put into C Libraries such as:
  - `musl`.
  - `glibc`.
  - Potentially: new LLVM `libc`.

[ ⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀ ]


### Ⅸ: (_Stretch_) WHATWG Encoding Functionality [ 0% ]

- The WHATWG (https://whatwg.org/) specifies many encodings which are required to support the web.
- Covers developing encodings to handle [encodings covered by the WHATWG Living Standard](https://encoding.spec.whatwg.org/).

[ ⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀ ]


### Ⅹ: (_Stretch_) Strong Exception Guarantee [ 0% ]

- `std::text<Encoding, NormalizationForm, Container>`: strong exception guarantee on all applicable operations.
- `noexcept` container support for `std::text` and `std::text_view`
  - `noexcept` allocator support.
  - Containers operations are made conditionally `noexcept` if possible based on the allocator and movability of the inserted types.

[ ⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀ ]
