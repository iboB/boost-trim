# Boost Trim

Trimmed-down [Boost](https://www.boost.org/). From 700MB to about 40 (~7MB zip). Only some headers are left in.

I use this for my projects that use Boost.Asio and Boost.Beast.

It would likely work for others.

Also a minimal CMakeLists.txt is added which adds the `IMPORTED` target `Boost::boost`.
