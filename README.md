<h1 align="center">
  🚀 press-ready
  <br/>
  <img alt="screencast" src="https://github.com/vibranthq/press-ready/blob/master/.readme/screencast.gif?raw=true">
</h1>

> Make your PDF compliant with press-ready PDF/X-1a.

## Pre-requisite

- Docker

## Quick Usage

Pull `vibranthq/press-ready` image from [Docker Hub](https://hub.docker.com/r/vibranthq/press-ready/).

Then run `docker run -it -v $PWD:/workdir vibranthq/press-ready --input <input filepath> --output <output filepath>`.

```bash
docker pull vibranthq/press-ready

docker run --rm -it \
  -v $PWD:/workdir \
  vibranthq/press-ready \
  --input ./input.pdf \
  --output ./output.pdf
```

Run `docker run --rm vibranthq/press-ready --help` to show help.

```bash
➜ docker run --rm vibranthq/press-ready --help
Options:
  --version          Show version number                               [boolean]
  --input            Input file path                                  [required]
  --output           Output file path                  [default: "./output.pdf"]
  --gray-scale       Use gray scale color space instead of CMYK
                                                      [boolean] [default: false]
  --enforce-outline  Convert embedded fonts to outlined fonts          [boolean]
  --boundary-boxes   Add boundary boxes on every page [boolean] [default: false]
  --help             Show help                                         [boolean]
```

## Options

### Color Mode

Press-ready will use **CMYK** by default. Give `--gray-scale` option to let them use **Grayscale** instead.

```bash
docker run --rm -it \
  -v ${CURDIR}:/workdir \
  vibranthq/press-ready \
  --input ./input.pdf \
  --output ./output.pdf \
  --gray-scale
```

### Boundary Boxes

Option `--boundary-boxes` will build TrimBox, CropBox and BleedBox on a generated PDF.

```bash
docker run --rm -it \
  -v ${CURDIR}:/workdir \
  vibranthq/press-ready \
  --input ./input.pdf \
  --output ./output.pdf \
  --boundary-boxes
```

### Outlined Fonts

You might not want to use this option since press-ready automatically guess whether embedded fonts should be outlined.
However, you can still control this behavior by passing `--enforce-outline` or `--no-enforce-outline`.

```bash
docker run --rm -it \
  -v ${CURDIR}:/workdir \
  vibranthq/press-ready \
  --input ./input.pdf \
  --output ./output.pdf \
  --enforce-outline
```

### Color Profile

Currently, there is only support for **Japan 2001 Coated**. If you have any suggestions, please consider submitting an issue.

## Tips

### Alias

Define an alias for press-ready as a shorthand command.

```bash
alias press-ready="docker run -it -v \$PWD:/workdir vibranthq/press-ready"
```

then you can run press-ready just like a normal command:

```bash
press-ready --help
press-ready --input <input.pdf> --output <output.pdf>
```

### Pull resource from AWS S3

Just run with S3 URL: `docker run -t vibranthq/press-ready <input s3url> <output s3url>`.

For fetching and uploading AWS S3 resources, you need to set env var `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY`.

```bash
docker run --rm -it \
  -e AWS_ACCESS_KEY_ID=<aws_key_id> \
  -e AWS_SECRET_ACCESS_KEY=<aws_secret> \
  vibranthq/press-ready s3://bucket/input.pdf s3://bucket/output.pdf
```

## Contribution

PRs are welcome. Make sure to do `make test` before filing pull requests.

### Development Build

```bash
make build
make test
make test-chrome
```

### Contributors

List of awesome contributors (generated by `git shortlog -sn`).

- Yasuaki Uechi
- Kenshi Muto
