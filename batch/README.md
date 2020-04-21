# Batch

Use cases

- Monte-carlo simulation / financial risk modeling
- VFX and 3D image rendering
- Media transcoding

## Components

- Storage account (storing input/output)
- Batch account (top level container)
- Pools (VM size & quantity)
- Jobs (logical group for tasks)
- Tasks (acutual items of work, e.g. commands)

## CLI

```
az batch pool create
```

```
az batch job create
```

```
az batch task create
```