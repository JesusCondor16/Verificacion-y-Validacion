# Verificacion-y-Validacion

Habiendo usado el SonarLint en un proyecto de sistema docente, en este caso, del módulo cursos ("AddCursoComponent.js"), se identificaron los siguiente problemas.

**Problema 1**

- La etiqueta <label> no tiene un atributo htmlFor que asocie el texto de la etiqueta con el control de entrada (<input>). Esto significa que el lector de pantalla y otras tecnologías de accesibilidad no podrán relacionar adecuadamente el texto de la etiqueta con el campo de entrada.

- Refactorización / Corrección:
Añadir htmlFor en la etiqueta <label> y asegurarse de que el id del <input> coincida: Esto asegura que la etiqueta esté asociada correctamente con el campo de entrada.


Fragmento de código
        <div className="form-group mb-2">
            <label htmlFor="cod_asignatura" className="form-label">Código de Asignatura</label>
            <input
             type="text"
             id="cod_asignatura"  // Añadido para vincular con el label
             placeholder="Digite el código de la asignatura"
             name="cod_asignatura"
             className="form-control"
             value={cod_asignatura}
             onChange={(e) => setCod_asignatura(e.target.value)}
             />
        </div>

**Problema 2**

- El componente AddCursoComponent recibe duplicate como una propiedad (prop), pero esta propiedad no está siendo validada. Esto es importante en React para garantizar que las propiedades se utilicen de manera correcta y evitar errores de tipo.

- Solución/Refactorizacion:
Puedes añadir validación de props utilizando PropTypes. De esta manera, le indicas al compilador o al IDE qué tipo de propiedad debe ser duplicate, y si es requerida o no.

- Fragmento de codigo:
    import React, { useState } from 'react';
    import PropTypes from 'prop-types'; // Importar PropTypes
    import { useNavigate, useParams } from 'react-router-dom';

    export const AddCursoComponent = ({ duplicate }) => {
        
        const [curso, setCurso] = useState({
            cod_asignatura: '',
            nombre_asignatura: '',
            tipo_asignatura: '',
            area_estudios: '',
            numero_semanas: '',
            horas_semanales: '',
            semestre_academico: '',
            ciclo: '',
            creditos: '',
            modalidad: '',
            prerequisitos: '',
            sumilla: '',
            evaluacion_aprendizaje: '',
            dia: '',
            hora_inicio: '',
            hora_fin: ''
        });

        const navigate = useNavigate();
        const { id } = useParams();


**Problema 3**

- La etiqueta <label> debe vincularse al campo de entrada mediante el atributo htmlFor para que el texto de la etiqueta esté correctamente asociado al control, lo que facilita su uso a personas que dependen de herramientas de asistencia, como los lectores de pantalla.

- Refactorización / Solución:
Para corregir este problema de accesibilidad, es recomendable añadir el atributo htmlFor en la etiqueta <label> y asegurarse de que el campo <input> tenga un id correspondiente. Esto no solo resolverá la advertencia de SonarLint, sino que también optimizará la accesibilidad y la experiencia del usuario en el formulario.

- Fragmento de codigo:

 <div className="form-group mb-2">
    <label htmlFor="semestre_academico" className="form-label">Semestre Académico</label>
    <input
        type="text"
        id="semestre_academico"  // Añadido para vincular con el label
        placeholder="Digite el semestre académico"
        name="semestre_academico"
        className="form-control"
        value={semestre_academico}
        onChange={(e) => setSemestre_academico(e.target.value)}
    />
</div>


**REPORTE ESTATICO**
1. AddCursoComponent
Problema: Múltiples variables de estado individuales

Descripción: El componente contiene muchas llamadas a useState, lo que dificulta la gestión del estado.
Corrección: Se agruparon todos los estados en un objeto curso, lo que simplifica la gestión y la legibilidad del código.
Problema: Falta de validación de props

Descripción: La propiedad duplicate no estaba validada, lo que podría resultar en errores en tiempo de ejecución.
Corrección: Se agregó validación de PropTypes para asegurar que duplicate es un booleano.
Problema: Manejo ineficiente de cambios en el estado

Descripción: Cada campo de entrada tenía su propia función de cambio.
Corrección: Se implementó una función handleChange para manejar los cambios de manera más eficiente, utilizando un solo manejador.
2. Campo "Código de Asignatura"
Problema: Falta de asociación entre <label> y <input>
Descripción: La etiqueta <label> no estaba asociada con el control de entrada, lo que afectaba la accesibilidad.
Corrección: Se añadió el atributo htmlFor en la etiqueta <label> y el atributo id en el <input> para vincularlos correctamente.
3. Campo "Semestre Académico"
Problema: Falta de asociación entre <label> y <input>
Descripción: Similar al campo "Código de Asignatura", la etiqueta no estaba asociada con el campo de entrada.
Corrección: Se implementó el mismo cambio que en el campo anterior, añadiendo htmlFor y id.
