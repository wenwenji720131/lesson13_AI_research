# Domain Masters

Use a domain master to decide scientific visual language. If the field is unknown or cross-disciplinary, create a one-off adaptive domain brief instead of forcing the content into an unsuitable style.

## Computer Science / Machine Learning

Use for model architecture, algorithm pipelines, LLM agents, multimodal systems, document processing, knowledge graphs, databases, information retrieval, software systems, and evaluation frameworks.

Visual language:
- Content communities: NeurIPS/ICML/ICLR for ML methods, CVPR/ICCV/ECCV for vision, ACL/EMNLP for NLP, WWW/KDD/SIGMOD/VLDB for web/KG/database/IR, USENIX/SOSP/OSDI/CHI for systems/HCI.
- Common entities: modules, tensors, token streams, embeddings, documents, graphs, databases, memory blocks, agents, tools, feedback loops, training/inference partitions.
- Good layouts: left-to-right pipeline, dual-stream fusion, central agent loop, hierarchical stack, input-method-output triptych, multi-panel ablation architecture.
- Style: clean academic vector diagram, soft tech pastels, precise arrows, thin outlines, controlled labels.
- Avoid: biomedical pathway style, generic dashboard collage, icon-pack infographic, marketing SaaS graphic, unexplained 3D objects.

## Materials / Chemistry

Use for electrochemistry, catalysis, crystal/interface mechanisms, molecular interactions, ion migration, polymers, batteries, solvents, membranes, and reaction pathways.

Visual language:
- Common entities: particles, ions, molecules, crystal lattices, layered materials, pores, electrodes, interfaces, solvation shells, reaction intermediates.
- Good layouts: macro-to-micro zoom, reaction path, before/after comparison, core-shell interface, parallel material comparison.
- Style: journal-grade materials schematic, precise shapes, low-saturation element colors, restrained texture, clear scale hierarchy.
- Avoid: fake microscopy, invented spectra, unsupported measurements, glossy product render, decorative chemistry icons.

## Biology / Medicine

Use for signaling pathways, cell mechanisms, tissue microenvironments, drug action, clinical workflow, omics pipeline, disease mechanism, and biomedical graphical abstracts.

Visual language:
- Common entities: cells, organelles, receptors, proteins, genes, pathways, tissues, vessels, immune cells, drug molecules, patient/sample flow.
- Good layouts: pathway cascade, cell-centered hub, tissue-to-cell zoom, treatment/control comparison, clinical sample-to-analysis pipeline.
- Style: clean BioRender-like academic schematic, readable labels, soft scientific palette, clear activation/inhibition arrows.
- Avoid: invented clinical outcomes, fake microscopy, unsupported biomarkers, overdramatic medical imagery, decorative anatomy.

## Unknown / Cross-Disciplinary Field

Use an adaptive brief:
- Identify reusable domain objects, process logic, scale, evidence boundaries, common figure conventions, and visual metaphors from the user text or reference image.
- Do not copy reference-image content, labels, data, logos, or exact proprietary composition.
- Keep the final prompt conservative: accurate objects, explicit modules, limited labels, and no invented evidence.
