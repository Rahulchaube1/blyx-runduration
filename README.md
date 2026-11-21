<img src="assets/logo.png" width="112" height="112" alt="RunDuration logo">

# RunDuration

Find the critical-path time in a forest of dependent tasks. This Blyx library is part of the packaging and code quality collection.

Adding workers cannot shorten a serial dependency chain. Compare total work with the longest dependency path before sizing a build pool. [Python, topological sorting](https://docs.python.org/3/library/graphlib.html)

## Install and run

Install [Blyx 0.2.1](https://www.blyx-lang.space/download) with a Rust toolchain and host linker for native builds.

```sh
git clone --depth 1 --branch v0.1.0 https://github.com/Rahulchaube1/blyx-runduration.git
cd blyx-runduration
blyxc native-run example.blyx
blyxc native-run tests.blyx
```

[Run the editable browser example](https://www.blyx-lang.space/play?example=package-runduration) · [Package page](https://www.blyx-lang.space/packages/runduration) · [Handbook](https://doc.blyx-lang.space/guide/albatross)

## Import the module

Run this in the directory containing your application's entry file.

```sh
git clone --depth 1 --branch v0.1.0 https://github.com/Rahulchaube1/blyx-runduration.git vendor/runduration
```

```blyx
use vendor::runduration::runduration;

fn main() {
    let parents = [-1, 0, 0, 2];
    let durations = [1, 3, 2, 5];
    let result = runduration_path(parents, durations);
    if len(result) == 0 { println!("invalid"); return; }
    let mut i = 0;
    while i < len(result) {
        println!(at(result, i));
        i += 1;
    }
}
```

Expected output

```text
8
3
11
```

## API

`runduration_path(parents, durations)`

Returns [longest path duration, first endpoint at that duration, total sequential work]. Each input row depends on one previous row or -1. Durations share a unit. Invalid arguments and nonfinite results return an empty vector. Integers carried in numeric vectors use the exact range from −(2^53−1) to 2^53−1.

| Argument | Domain |
| --- | --- |
| parents | Vector of values, each a exact signed integer |
| durations | Vector of values, each a nonnegative finite number |

## In use

[Albatross](https://github.com/Rahulchaube1/blyx-albatross) uses this module to estimate a build forest's scheduling lower bound from dependencies and worker capacity.

## Verification and contributions

The regression suite in [tests.blyx](tests.blyx) checks the example, boundary cases and invalid inputs. Include a short reproducer and your compiler version in [an issue](https://github.com/Rahulchaube1/blyx-runduration/issues). The source is dual-licensed under [MIT](LICENSE-MIT) or [Apache-2.0](LICENSE-APACHE). The package artwork uses [Lucide icons](https://lucide.dev/license); see [artwork notices](assets/NOTICE.txt).

## Connect with Rahul Chaube

[Portfolio](https://www.rahulchaube1.com/) · [GitHub](https://github.com/Rahulchaube1) · [LinkedIn](https://www.linkedin.com/in/rahulchaube1) · [Hugging Face](https://huggingface.co/oncody) · [X](https://x.com/RahulChaube_) · [EverestQ](https://www.everestqai.com/) · [Contact](https://www.rahulchaube1.com/contact)

[Blyx website](https://www.blyx-lang.space/) · [BlyxTorch](https://www.blyx-lang.space/packages/blyxtorch) · [Handbook](https://doc.blyx-lang.space/) · [Community](https://www.blyx-lang.space/community)

Support Rahul’s open-source work through [GitHub Sponsors](https://github.com/sponsors/Rahulchaube1) or [Buy Me a Coffee](https://buymeacoffee.com/rahulchaube).
