# Introduction to 3D Vision

## 3D representation 
- Point Cloud : dimensions = N X 3
- Voxel : 3D grid , assigning values (0 or 1)
- Mesh : Kind of a graph with **vertices** (N X 3) with **edges** connecting them . Also a **face** consisting of triangles
- Implicit : Kind of like a distance function (SDF) with values < 0 inside and >0 inside and =0 being boundary. 

## File Formats
- Obj : Basically a text file , containing the position of each vertex , the UV position o f each texture coordinate , their normals and faces
- Ply : Binary encoded ; Efficent for storing data ; Not recommended for texture meshes

## Major research areas
- ### 3D reconstruction from a single image
- ### 3D reconstruction from multi-view image
- ### 3D reconstruction from text
- ### Temporal Consistent reconstruction of humans
- ### Garment extraction from single image
- ### CLoth Simulation
- ### UV Parameterization and Texture Mapping
- ### Hand Object Interaction

## Tools and Librarires
### Meshlab / PyMeshlab ( The python version )
- Link to Colab : https://colab.research.google.com/drive/13K0uyazGpzCFrPZZhh-ucp61famoLWC7#scrollTo=ig6kCSsoUPth
- Loading and Visualising obj 
    - ms.load_new_mesh(os.path.join(src, 'bunny/mesh/bunny_no_texture.obj'))
- Changing certain properties of image like color etc
    - ms.set_color_per_vertex(color1=color) 
- Conditioning on a property
    - ms.compute_selection_by_condition_per_face(condselect=condition)
- Property transfer
    - ms.transfer_attributes_per_vertex
- Poission Sampling and Reconstruction to remove noise
    - ms.generate_sampling_poisson_disk(samplenum=5000)
    - ms.generate_surface_reconstruction_screened_poisson()
- Morphing
    - ms.compute_coord_linear_morphing(targetmesh=0,percentmorph=80)

### Open3D
- Link to Colab : https://colab.research.google.com/drive/18kO1EKWUR0bg0JhiYilwJ_JJBKu8ck4k#scrollTo=35FrJ90ytZ_a
- Contains information about points and triangles as an array
    - o3d.io.read_point_cloud
    - o3d.io.read_triangle_mesh