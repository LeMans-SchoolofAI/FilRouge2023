<p>Quelques retours pour se lancer avec tensorflow_similarity.</p>
<p> En particulier, nous nous sommes rendu compte que la version maître à date 0.17.1 ne concordait pas forcément à ce qui était disponible dans le tutoriel de TF. Idem pour les autres branches.</p></br>
<p> Pour la mise en place, du plus simple au plus complexe: Collab >> WSL >> Linex/Ubuntu >> Windows </p>
</br>
<p> Sur votre machine pour utiliser GPU: https://www.tensorflow.org/install/gpu?hl=fr </p>
<p> Il est préconisé d'avoir la page github du repo utilisé pour le tutoriel pas très loin pour récupérer les scripts manquants danas tensorflow_similarity==0.17.1</p>

<h2>Windows</h2>
<h3>Installation</h3>
<p>-> il a fallu installer Microsoft C++ studio</br>
-> il a fallu reconstruire une version de nmsbuild avant l'installation de tensorflow_similarity (https://github.com/nmslib/nmslib/issues/538):</br>
</br>
pip install --upgrade pybind11        # 2.10.1 or higher  (latest as of today: 2.11.1)
pip install --verbose  'nmslib @ git+https://github.com/nmslib/nmslib.git#egg=nmslib&subdirectory=python_bindings'
</br>
</p>

<h3> Utilisation </h3>
<li>Le package tensorflow_similarity cherche resource qui semble ne pas exister avec windows mais plutôt ubuntu à l'installation de python (?). Une modif à faire dans tensorflow_similarity tensorflow_datasets/core/shuffle.py: https://github.com/tensorflow/datasets/commit/82215c7cf4b3e6df706a72c9b7ad8cede09f4d84 </li></br>
<li>Dans la compilation du modèle issu de tfsim_architectures.EfficientNetSim il n'y a de search 'linear' prévu en v0.17.1 mais plutôt nmslib (=Non-Metric Space Library : An efficient similarity search library and a toolkit for evaluation of k-NN methods for generic non-metric spaces). Il faut donc le préciser à la place de linear: </br>
# compiling and training</br>
model.compile(</br>
    optimizer=tf.keras.optimizers.Adam(LR),</br>
    loss=loss,</br>
    distance=distance,</br>
    search='nmslib',</br>
)</br>
</li>
