# Desarrollo de herramienta para caracterización de amenazas basada en ML.

Este proyecto tiene como objetivo hacer un Fine-Tuning de un LLM para la tarea de identificación automática de Tácticas, Técnicas y Procedimientos (TTPs) a partir de logs de sistema y aplicaciones.

La técnica empleada para fine-tuning ha sido QLoRA, mediante un enfoque de Supervised Fine Tuning. Para ello, se ha utilizado la librería Unsloth. Este proyecto fue realizado con una GPU L4, pero puede hacerse en cualquier gráfica con aproximadamente 15GB de RAM.

El modelo base es Llama 3 8B instruct, versión cuantizada a 4 bits de Unsloth.

El dataset utilizado fue Linux-APT Dataset 2024.

Este dataset fue desarrollado en una infraestructura con el SIEM Wazuh, por lo que se utiliza 3 campos (description, location y level) de las alertas de Wazuh, además del log en sí, para dar contexto al LLM.

Los ataques simulados en el dataset pertenecen a los grupos APT41, APT28, APT29 y Turla APT, así como ataques relacionados con la vulnerabilidad de Apache Struts

Se compone de los siguientes archivos:

- data_processing.ipynb: preprocesa el dataset antes mencionado para elegir las cabeceras interesantes. Las features son: "source", "description", "level" y "full_log"; y las etiquetas son "tactics" y "techniques".

- fine_tune_unsloth.ipynb: se hace el entrenamiento con el dataset de train y almacena los adapters de LoRA.

- evaluation.ipynb: se evalua la precisión del modelo con el dataset de test.

Cabe destacar que los trozos de código en los que se sube al repositorio de bfrenan de HuggingFace (método push_to_hub), no se podrán hacer ya que el token no es válido. En caso de quererse hacer, cambiar token y repositorio.
