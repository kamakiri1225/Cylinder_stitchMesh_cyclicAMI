# Cylinder_stitchMesh_cyclicAMI

## メッシュ作成

- mesh001
- mesh002
![image](https://user-images.githubusercontent.com/36812492/231796658-383046f9-5d4d-4b15-80ac-be558389777b.png)

[【OpenFOAM】円筒形状の異なるメッシュの境界を結合する](https://takun-physics.net/15911/)
## mesh001

```bash
blockMesh
```

## mesh002
```bash
blockMesh
transformPoints -translate '(0 0 0.101)'
```
mesh002はblockMesh後にz方向101mm平行移動しておきます。

## メッシュを合体
```bash
cp -r mesh001 mergeMesh001_002
mergeMeshes -overwrite mergeMesh001_002 mesh002
```

## メッシュを結合
```bash
cp -r mergeMesh001_002 stitchMesh001_002
cd stitchMesh001_002
stitchMesh -overwrite outlet_inlet inlet_outlet
```
![image](https://user-images.githubusercontent.com/36812492/231797698-5f60fb70-eadd-47c1-9a56-e4490a4ca4d9.png)

## 円筒内流れ（stitchMesh)
- stitchMesh001_002_laminar

[【OpenFOAM】異なるメッシュの境界を結合した後で円筒内の流れ](https://takun-physics.net/15957/)


## 円筒内流れ(cyclicAMI)
- mergeMesh001_002_cyclicAMI_laminar

[【OpenFOAM(cyclicAMI)】異なるメッシュの境界で円筒内の流れ](https://takun-physics.net/15942/)

- 層流条件: $\nu$ $= 5 \times 10^{-3}$
- 乱流条件: $\nu$ $= 5 \times 10^{-6}$
