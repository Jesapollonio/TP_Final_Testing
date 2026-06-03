<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>DentalTime - Documentación Interactiva</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <style>
        body {
            background-color: #f8fafc;
            color: #0f172a;
        }
        .chart-container {
            position: relative;
            width: 100%;
            max-width: 500px;
            margin-left: auto;
            margin-right: auto;
            height: 300px;
            max-height: 350px;
        }
        @media (min-width: 768px) {
            .chart-container {
                height: 350px;
            }
        }
        .hide-scroll::-webkit-scrollbar {
            display: none;
        }
        .hide-scroll {
            -ms-overflow-style: none;
            scrollbar-width: none;
        }
        .step-transition {
            transition: all 0.3s ease-in-out;
        }
        .nav-active {
            background-color: #0f766e;
            color: white;
            font-weight: bold;
        }
        .nav-inactive {
            background-color: transparent;
            color: #94a3b8;
        }
        .nav-inactive:hover {
            background-color: #1e293b;
            color: #f1f5f9;
        }
    </style>
    <!-- Chosen Palette: Dental Clean (Teal #0d9488 & Slate #1e293b, Neutral backgrounds) -->
    <!-- Application Structure Plan: La aplicación utiliza una estructura de 'Dashboard Documental'. Se divide en una barra de navegación lateral para acceso rápido y un área de contenido principal dinámica. Esta estructura no lineal permite a los desarrolladores y stakeholders saltar directamente a la información de su interés (arquitectura, flujos, pruebas) sin tener que hacer scroll por un documento plano. Los datos estáticos del README se han transformado en tarjetas, visualizaciones por pasos y diagramas de estado interactivos para mejorar la retención cognitiva y la exploración del sistema DentalTime. -->
    <!-- Visualization & Content Choices: 
         - Requerimientos -> Inform -> Tarjetas de cuadrícula (HTML/Tailwind) -> Interacción de hover -> Facilita la lectura escaneable.
         - Arquitectura/Entidades -> Organize -> Pestañas y paneles de detalles dinámicos (JS) -> Evita la sobrecarga de información, revelando detalles bajo demanda. No SVG.
         - Secuencias UML -> Process -> Línea de tiempo interactiva paso a paso (JS/HTML) -> Permite comprender la lógica de validación de colisiones de forma secuencial y controlada.
         - Suite de Tests -> Inform/Compare -> Gráfico de Anillo (Chart.js) -> Representación visual del 100% de cobertura y listado de casos, proporcionando un impacto visual inmediato sobre la calidad del software. -->
    <!-- CONFIRMATION: NO SVG graphics used. NO Mermaid JS used. -->
</head>
<body class="flex h-screen overflow-hidden font-sans antialiased">

    <aside class="w-64 bg-slate-900 flex-shrink-0 flex flex-col h-full hidden md:flex z-20">
        <div class="h-16 flex items-center px-6 bg-slate-950 border-b border-slate-800">
            <span class="text-2xl mr-2">🦷</span>
            <h1 class="text-white text-lg font-bold tracking-wide">DentalTime Docs</h1>
        </div>
        <nav class="flex-1 overflow-y-auto py-4 space-y-1 px-3">
            <button onclick="navigate('overview')" id="nav-overview" class="nav-btn w-full text-left px-4 py-3 rounded-lg nav-active flex items-center transition-colors">
                <span class="mr-3 text-lg">📊</span> Resumen del Sistema
            </button>
            <button onclick="navigate('architecture')" id="nav-architecture" class="nav-btn w-full text-left px-4 py-3 rounded-lg nav-inactive flex items-center transition-colors">
                <span class="mr-3 text-lg">🏢</span> Arquitectura y Datos
            </button>
            <button onclick="navigate('workflows')" id="nav-workflows" class="nav-btn w-full text-left px-4 py-3 rounded-lg nav-inactive flex items-center transition-colors">
                <span class="mr-3 text-lg">🔄</span> Flujos Dinámicos
            </button>
            <button onclick="navigate('quality')" id="nav-quality" class="nav-btn w-full text-left px-4 py-3 rounded-lg nav-inactive flex items-center transition-colors">
                <span class="mr-3 text-lg">🧪</span> Calidad y Tests
            </button>
            <button onclick="navigate('deploy')" id="nav-deploy" class="nav-btn w-full text-left px-4 py-3 rounded-lg nav-inactive flex items-center transition-colors">
                <span class="mr-3 text-lg">🚀</span> Despliegue
            </button>
        </nav>
        <div class="p-4 border-t border-slate-800 text-xs text-slate-500">
            Python 3.10+ | Tkinter UI<br>
            Clean Architecture
        </div>
    </aside>

    <main class="flex-1 h-full overflow-y-auto bg-slate-50 relative hide-scroll">
        
        <header class="md:hidden bg-slate-900 h-16 flex items-center justify-between px-4 sticky top-0 z-30">
            <div class="flex items-center">
                <span class="text-2xl mr-2">🦷</span>
                <h1 class="text-white text-lg font-bold">DentalTime</h1>
            </div>
            <select id="mobile-nav" onchange="navigate(this.value)" class="bg-slate-800 text-white border-none rounded p-1 text-sm outline-none">
                <option value="overview">Resumen</option>
                <option value="architecture">Arquitectura</option>
                <option value="workflows">Flujos</option>
                <option value="quality">Calidad</option>
                <option value="deploy">Despliegue</option>
            </select>
        </header>

        <div class="p-6 md:p-10 max-w-6xl mx-auto pb-24">
            
            <section id="view-overview" class="view-section block animate-fade-in">
                <div class="mb-8">
                    <h2 class="text-3xl font-bold text-slate-800 mb-4">Resumen del Sistema</h2>
                    <p class="text-lg text-slate-600 bg-white p-6 rounded-xl border border-slate-200 shadow-sm leading-relaxed">
                        Esta sección presenta el objetivo principal y los requerimientos clave del software <strong>DentalTime</strong>. Aquí encontrará la base conceptual de la aplicación, diseñada para optimizar y robustecer el flujo operacional de reserva de turnos, mitigando colisiones horarias y garantizando un orden cronológico exacto mediante Python y Tkinter.
                    </p>
                </div>

                <h3 class="text-xl font-bold text-teal-700 border-b-2 border-teal-100 pb-2 mb-6">Requerimientos Funcionales Críticos (RF)</h3>
                <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6 mb-10">
                    <div class="bg-white p-5 rounded-xl border border-slate-200 shadow-sm hover:shadow-md transition-shadow">
                        <div class="text-3xl mb-3">👤</div>
                        <h4 class="font-bold text-slate-800 mb-2">RF-01: Registro Pacientes</h4>
                        <p class="text-sm text-slate-600">Captura obligatoria de Nombre, Apellido, ID/DNI y teléfono de contacto válido.</p>
                    </div>
                    <div class="bg-white p-5 rounded-xl border border-slate-200 shadow-sm hover:shadow-md transition-shadow ring-2 ring-teal-500 ring-offset-2">
                        <div class="text-3xl mb-3">🛡️</div>
                        <h4 class="font-bold text-slate-800 mb-2">RF-02: Prevención Colisiones</h4>
                        <p class="text-sm text-slate-600">Prohibición estricta de superposición horaria parcial o total usando validación algorítmica de intervalos.</p>
                    </div>
                    <div class="bg-white p-5 rounded-xl border border-slate-200 shadow-sm hover:shadow-md transition-shadow">
                        <div class="text-3xl mb-3">⏱️</div>
                        <h4 class="font-bold text-slate-800 mb-2">RF-03: Ordenamiento Activo</h4>
                        <p class="text-sm text-slate-600">Registros mantenidos en orden cronológico automático desde el más próximo al más lejano.</p>
                    </div>
                    <div class="bg-white p-5 rounded-xl border border-slate-200 shadow-sm hover:shadow-md transition-shadow">
                        <div class="text-3xl mb-3">❌</div>
                        <h4 class="font-bold text-slate-800 mb-2">RF-04: Cancelación Eficiente</h4>
                        <p class="text-sm text-slate-600">Eliminación física del turno mediante búsqueda insensible a mayúsculas (por DNI o Nombre).</p>
                    </div>
                    <div class="bg-white p-5 rounded-xl border border-slate-200 shadow-sm hover:shadow-md transition-shadow">
                        <div class="text-3xl mb-3">🔍</div>
                        <h4 class="font-bold text-slate-800 mb-2">RF-05: Búsqueda en Tiempo Real</h4>
                        <p class="text-sm text-slate-600">Filtrado dinámico de la agenda por nombre, ID, tratamiento o fecha de la cita.</p>
                    </div>
                </div>

                <h3 class="text-xl font-bold text-slate-700 border-b-2 border-slate-200 pb-2 mb-6">Requerimientos No Funcionales (RNF)</h3>
                <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
                    <div class="bg-slate-800 text-white p-5 rounded-xl shadow-md">
                        <h4 class="font-bold text-teal-400 mb-2">RNF-01: Portabilidad</h4>
                        <p class="text-sm text-slate-300">Sin dependencias externas. UI construida exclusivamente con Tkinter/ttk estándar para ejecución en Windows/Linux/macOS.</p>
                    </div>
                    <div class="bg-slate-800 text-white p-5 rounded-xl shadow-md">
                        <h4 class="font-bold text-teal-400 mb-2">RNF-02: Eficiencia O(n log n)</h4>
                        <p class="text-sm text-slate-300">Ordenación garantizada mediante el algoritmo Timsort nativo de Python para la gestión de turnos.</p>
                    </div>
                    <div class="bg-slate-800 text-white p-5 rounded-xl shadow-md">
                        <h4 class="font-bold text-teal-400 mb-2">RNF-03: Tipos Nativos</h4>
                        <p class="text-sm text-slate-300">Tratamiento de fechas sustentado en el módulo datetime, descartando fallos semánticos por texto plano.</p>
                    </div>
                </div>
            </section>

            <section id="view-architecture" class="view-section hidden animate-fade-in">
                <div class="mb-8">
                    <h2 class="text-3xl font-bold text-slate-800 mb-4">Arquitectura y Entidades</h2>
                    <p class="text-lg text-slate-600 bg-white p-6 rounded-xl border border-slate-200 shadow-sm leading-relaxed">
                        Esta sección detalla el diseño interno del software. Permite explorar el modelo conceptual basado en <strong>Clean Architecture</strong> y las tres entidades de dominio que sustentan las reglas de negocio. Seleccione una capa arquitectónica o una entidad para descubrir sus propiedades específicas.
                    </p>
                </div>

                <div class="grid grid-cols-1 lg:grid-cols-2 gap-8 mb-10">
                    <div class="bg-white rounded-xl border border-slate-200 shadow-sm overflow-hidden flex flex-col">
                        <div class="bg-slate-100 p-4 border-b border-slate-200 font-bold text-slate-700 flex items-center">
                            <span class="mr-2">🏗️</span> Capas del Sistema (Monolítico Modular)
                        </div>
                        <div class="flex flex-col sm:flex-row h-full">
                            <div class="w-full sm:w-2/5 bg-slate-50 border-r border-slate-200 flex flex-col p-2 gap-2">
                                <button onclick="showLayer('presentation')" id="btn-layer-presentation" class="layer-btn text-left p-3 rounded-md bg-teal-600 text-white font-medium transition-colors">3. Presentación (UI)</button>
                                <button onclick="showLayer('application')" id="btn-layer-application" class="layer-btn text-left p-3 rounded-md bg-slate-200 text-slate-700 hover:bg-slate-300 transition-colors">2. Aplicación</button>
                                <button onclick="showLayer('domain')" id="btn-layer-domain" class="layer-btn text-left p-3 rounded-md bg-slate-200 text-slate-700 hover:bg-slate-300 transition-colors">1. Dominio</button>
                            </div>
                            <div class="w-full sm:w-3/5 p-6 flex items-center justify-center bg-white" id="layer-content">
                                <div class="text-center">
                                    <h4 class="text-xl font-bold text-slate-800 mb-3">Capa de Presentación</h4>
                                    <p class="text-slate-600 text-sm leading-relaxed">Representada por la interfaz <strong>DentalTimeGUI</strong>. Traduce las entradas de usuario, captura eventos y actualiza la vista interactiva mediante enlaces directos a la capa de aplicación.</p>
                                </div>
                            </div>
                        </div>
                    </div>

                    <div class="bg-white rounded-xl border border-slate-200 shadow-sm overflow-hidden flex flex-col">
                        <div class="bg-teal-900 p-4 border-b border-teal-800 font-bold text-white flex items-center">
                            <span class="mr-2">🗃️</span> Entidades de Dominio
                        </div>
                        <div class="p-4 border-b border-slate-100 flex gap-2 overflow-x-auto hide-scroll">
                            <button onclick="showEntity('consultorio')" id="btn-ent-consultorio" class="ent-btn px-4 py-2 bg-teal-100 text-teal-800 font-bold rounded-full whitespace-nowrap transition-colors">Consultorio</button>
                            <button onclick="showEntity('turno')" id="btn-ent-turno" class="ent-btn px-4 py-2 bg-slate-100 text-slate-600 rounded-full whitespace-nowrap hover:bg-slate-200 transition-colors">Turno</button>
                            <button onclick="showEntity('paciente')" id="btn-ent-paciente" class="ent-btn px-4 py-2 bg-slate-100 text-slate-600 rounded-full whitespace-nowrap hover:bg-slate-200 transition-colors">Paciente</button>
                        </div>
                        <div class="p-6 bg-slate-50 flex-1" id="entity-content">
                            <h4 class="text-lg font-bold text-slate-800 mb-1">Consultorio</h4>
                            <p class="text-sm text-slate-500 mb-4 italic">Clase contenedora principal (Raíz)</p>
                            <table class="w-full text-sm text-left">
                                <thead class="bg-slate-200 text-slate-700">
                                    <tr><th class="p-2 rounded-tl-md">Atributo</th><th class="p-2">Tipo</th><th class="p-2 rounded-tr-md">Descripción</th></tr>
                                </thead>
                                <tbody>
                                    <tr class="border-b border-slate-200"><td class="p-2 font-mono text-xs">nombre</td><td class="p-2 text-teal-700">str</td><td class="p-2">Nombre de la clínica dental.</td></tr>
                                    <tr><td class="p-2 font-mono text-xs">lista_turnos</td><td class="p-2 text-teal-700">list[Turno]</td><td class="p-2">Colección cronológica centralizada de citas activas (1 a Muchos).</td></tr>
                                </tbody>
                            </table>
                        </div>
                    </div>
                </div>
            </section>

            <section id="view-workflows" class="view-section hidden animate-fade-in">
                <div class="mb-8">
                    <h2 class="text-3xl font-bold text-slate-800 mb-4">Flujos Dinámicos (UML Secuencia)</h2>
                    <p class="text-lg text-slate-600 bg-white p-6 rounded-xl border border-slate-200 shadow-sm leading-relaxed">
                        Esta sección traduce los diagramas de secuencia UML estáticos en una experiencia paso a paso. Interactúe con los controles inferiores para visualizar cómo interactúan los componentes (GUI, Controlador y Modelos) durante las operaciones críticas de <strong>Agendamiento</strong> y <strong>Cancelación</strong>.
                    </p>
                </div>

                <div class="flex justify-center mb-6 space-x-4">
                    <button onclick="loadWorkflow('agendar')" id="btn-wf-agendar" class="px-6 py-2 rounded-lg bg-teal-600 text-white font-bold shadow-md hover:bg-teal-700 transition-colors">Flujo: Agendar Turno</button>
                    <button onclick="loadWorkflow('cancelar')" id="btn-wf-cancelar" class="px-6 py-2 rounded-lg bg-slate-200 text-slate-700 font-bold hover:bg-slate-300 transition-colors">Flujo: Cancelar Turno</button>
                </div>

                <div class="bg-white rounded-xl border border-slate-200 shadow-lg p-6 relative min-h-[400px] flex flex-col justify-between">
                    <div>
                        <h3 id="wf-title" class="text-2xl font-bold text-slate-800 mb-2">Agendar Turno (Validación Segura)</h3>
                        <p id="wf-desc" class="text-slate-500 mb-8 border-b border-slate-100 pb-4">Proceso de validación temporal antes de confirmar y agregar una nueva cita a la agenda.</p>
                        
                        <div class="relative px-4">
                            <div class="absolute left-8 top-0 bottom-0 w-1 bg-slate-200 rounded"></div>
                            
                            <div id="wf-step-container" class="space-y-6 relative z-10">
                            </div>
                        </div>
                    </div>
                    
                    <div class="mt-10 flex justify-between items-center bg-slate-50 p-4 rounded-lg border border-slate-200">
                        <button onclick="prevStep()" id="btn-prev-step" class="px-4 py-2 bg-slate-300 text-slate-700 rounded disabled:opacity-50 disabled:cursor-not-allowed font-medium" disabled>⬅ Paso Anterior</button>
                        <span id="step-indicator" class="font-bold text-teal-700">Paso 1 de 4</span>
                        <button onclick="nextStep()" id="btn-next-step" class="px-4 py-2 bg-teal-600 text-white rounded hover:bg-teal-700 disabled:opacity-50 disabled:cursor-not-allowed font-medium">Siguiente Paso ➡</button>
                    </div>
                </div>
            </section>

            <section id="view-quality" class="view-section hidden animate-fade-in">
                <div class="mb-8">
                    <h2 class="text-3xl font-bold text-slate-800 mb-4">Plan de Calidad y Suite de Tests</h2>
                    <p class="text-lg text-slate-600 bg-white p-6 rounded-xl border border-slate-200 shadow-sm leading-relaxed">
                        Esta sección presenta el estado de salud del código base. La estabilidad de las reglas de negocio de DentalTime se garantiza mediante una suite de pruebas unitarias integradas (basadas en <code>unittest</code>). Se evalúan las condiciones límite y los flujos felices del negocio para garantizar <strong>100% de cobertura</strong> en colisiones lógicas.
                    </p>
                </div>

                <div class="grid grid-cols-1 lg:grid-cols-3 gap-8">
                    <div class="col-span-1 lg:col-span-1 bg-white p-6 rounded-xl border border-slate-200 shadow-sm flex flex-col items-center justify-center">
                        <h3 class="text-lg font-bold text-slate-700 mb-4">Cobertura de la Suite</h3>
                        <div class="chart-container">
                            <canvas id="qualityChart"></canvas>
                        </div>
                        <div class="mt-6 text-center">
                            <span class="inline-block px-4 py-1 bg-green-100 text-green-800 rounded-full font-bold text-sm tracking-wide">ESTADO: ESTABLE</span>
                        </div>
                    </div>

                    <div class="col-span-1 lg:col-span-2 bg-white rounded-xl border border-slate-200 shadow-sm overflow-hidden">
                        <div class="bg-slate-800 p-4 flex justify-between items-center">
                            <h3 class="font-bold text-white">Casos de Prueba (Unittest)</h3>
                            <span class="text-xs text-slate-400 font-mono">Total: 7 Casos</span>
                        </div>
                        <div class="overflow-x-auto">
                            <table class="w-full text-sm text-left">
                                <thead class="bg-slate-100 text-slate-600 border-b border-slate-200">
                                    <tr>
                                        <th class="p-3">ID</th>
                                        <th class="p-3">Componente</th>
                                        <th class="p-3">Escenario Evaluado</th>
                                        <th class="p-3 text-center">Estado</th>
                                    </tr>
                                </thead>
                                <tbody>
                                    <tr class="border-b border-slate-100 hover:bg-slate-50">
                                        <td class="p-3 font-bold text-slate-700">UT-01</td>
                                        <td class="p-3 font-mono text-xs text-teal-700">Paciente.__init__</td>
                                        <td class="p-3 text-slate-600">Creación con campos obligatorios en blanco.</td>
                                        <td class="p-3 text-center"><span class="px-2 py-1 bg-green-100 text-green-700 rounded text-xs font-bold">PASSED</span></td>
                                    </tr>
                                    <tr class="border-b border-slate-100 hover:bg-slate-50">
                                        <td class="p-3 font-bold text-slate-700">UT-02</td>
                                        <td class="p-3 font-mono text-xs text-teal-700">Consultorio.agendar_turno</td>
                                        <td class="p-3 text-slate-600">Inserción en bloque completamente disponible.</td>
                                        <td class="p-3 text-center"><span class="px-2 py-1 bg-green-100 text-green-700 rounded text-xs font-bold">PASSED</span></td>
                                    </tr>
                                    <tr class="border-b border-slate-100 hover:bg-slate-50">
                                        <td class="p-3 font-bold text-slate-700">UT-03</td>
                                        <td class="p-3 font-mono text-xs text-teal-700">Consultorio.agendar_turno</td>
                                        <td class="p-3 text-slate-600">Denegar asignación en fechas/horas pasadas.</td>
                                        <td class="p-3 text-center"><span class="px-2 py-1 bg-green-100 text-green-700 rounded text-xs font-bold">PASSED</span></td>
                                    </tr>
                                    <tr class="border-b border-slate-100 hover:bg-slate-50">
                                        <td class="p-3 font-bold text-slate-700">UT-04</td>
                                        <td class="p-3 font-mono text-xs text-teal-700">Consultorio.agendar_turno</td>
                                        <td class="p-3 text-slate-600">Bloqueo por duplicidad de horario exacta.</td>
                                        <td class="p-3 text-center"><span class="px-2 py-1 bg-green-100 text-green-700 rounded text-xs font-bold">PASSED</span></td>
                                    </tr>
                                    <tr class="border-b border-slate-100 hover:bg-slate-50">
                                        <td class="p-3 font-bold text-slate-700">UT-05</td>
                                        <td class="p-3 font-mono text-xs text-teal-700">Consultorio.agendar_turno</td>
                                        <td class="p-3 text-slate-600">Bloqueo por solapamiento parcial de minutos.</td>
                                        <td class="p-3 text-center"><span class="px-2 py-1 bg-green-100 text-green-700 rounded text-xs font-bold">PASSED</span></td>
                                    </tr>
                                    <tr class="border-b border-slate-100 hover:bg-slate-50">
                                        <td class="p-3 font-bold text-slate-700">UT-06</td>
                                        <td class="p-3 font-mono text-xs text-teal-700">Consultorio.mostrar_turnos</td>
                                        <td class="p-3 text-slate-600">Ordenamiento automático de menor a mayor.</td>
                                        <td class="p-3 text-center"><span class="px-2 py-1 bg-green-100 text-green-700 rounded text-xs font-bold">PASSED</span></td>
                                    </tr>
                                    <tr class="hover:bg-slate-50">
                                        <td class="p-3 font-bold text-slate-700">UT-07</td>
                                        <td class="p-3 font-mono text-xs text-teal-700">Consultorio.cancelar_turno</td>
                                        <td class="p-3 text-slate-600">Eliminación efectiva (búsqueda case-insensitive).</td>
                                        <td class="p-3 text-center"><span class="px-2 py-1 bg-green-100 text-green-700 rounded text-xs font-bold">PASSED</span></td>
                                    </tr>
                                </tbody>
                            </table>
                        </div>
                    </div>
                </div>
            </section>

            <section id="view-deploy" class="view-section hidden animate-fade-in">
                <div class="mb-8">
                    <h2 class="text-3xl font-bold text-slate-800 mb-4">Instrucciones de Despliegue</h2>
                    <p class="text-lg text-slate-600 bg-white p-6 rounded-xl border border-slate-200 shadow-sm leading-relaxed">
                        Esta sección detalla los pasos finales para la ejecución del software en un entorno local, destacando su naturaleza libre de dependencias complejas al utilizar las herramientas nativas de Python.
                    </p>
                </div>

                <div class="space-y-6">
                    <div class="bg-white p-6 rounded-xl border border-slate-200 shadow-sm flex items-start">
                        <div class="bg-slate-100 text-slate-800 text-xl font-bold w-12 h-12 flex items-center justify-center rounded-lg mr-4 shrink-0">1</div>
                        <div class="w-full">
                            <h3 class="text-xl font-bold text-slate-800 mb-2">Clonar el Repositorio</h3>
                            <p class="text-slate-600 mb-3 text-sm">Descargue el código fuente directamente desde GitHub a su entorno local.</p>
                            <div class="bg-slate-900 rounded p-4 overflow-x-auto">
                                <code class="text-teal-400 font-mono text-sm">git clone https://github.com/tu-usuario/dentaltime.git<br>cd dentaltime</code>
                            </div>
                        </div>
                    </div>

                    <div class="bg-white p-6 rounded-xl border border-slate-200 shadow-sm flex items-start">
                        <div class="bg-slate-100 text-slate-800 text-xl font-bold w-12 h-12 flex items-center justify-center rounded-lg mr-4 shrink-0">2</div>
                        <div class="w-full">
                            <h3 class="text-xl font-bold text-slate-800 mb-2">Ejecutar la Aplicación Gráfica (GUI)</h3>
                            <p class="text-slate-600 mb-3 text-sm">Inicie la interfaz gráfica. No se requiere <code>pip install</code> adicional gracias al uso de <code>tkinter</code>.</p>
                            <div class="bg-slate-900 rounded p-4 overflow-x-auto">
                                <code class="text-green-400 font-mono text-sm">python app.py</code>
                            </div>
                        </div>
                    </div>

                    <div class="bg-white p-6 rounded-xl border border-slate-200 shadow-sm flex items-start">
                        <div class="bg-slate-100 text-slate-800 text-xl font-bold w-12 h-12 flex items-center justify-center rounded-lg mr-4 shrink-0">3</div>
                        <div class="w-full">
                            <h3 class="text-xl font-bold text-slate-800 mb-2">Ejecución Continua de Tests</h3>
                            <p class="text-slate-600 mb-3 text-sm">Para integraciones CI/CD o auditorías en consola, ejecute la suite de calidad aislando la GUI mediante un flag.</p>
                            <div class="bg-slate-900 rounded p-4 overflow-x-auto">
                                <code class="text-blue-400 font-mono text-sm">python app.py --test</code>
                            </div>
                        </div>
                    </div>
                </div>
            </section>
        </div>
    </main>

    <script>
        const views = ['overview', 'architecture', 'workflows', 'quality', 'deploy'];
        let chartInstance = null;

        function navigate(viewId) {
            views.forEach(v => {
                document.getElementById('view-' + v).classList.add('hidden');
                document.getElementById('view-' + v).classList.remove('block');
                
                const navBtn = document.getElementById('nav-' + v);
                if(navBtn) {
                    navBtn.classList.remove('nav-active');
                    navBtn.classList.add('nav-inactive');
                }
            });

            document.getElementById('view-' + viewId).classList.remove('hidden');
            document.getElementById('view-' + viewId).classList.add('block');
            
            const activeNavBtn = document.getElementById('nav-' + viewId);
            if(activeNavBtn) {
                activeNavBtn.classList.remove('nav-inactive');
                activeNavBtn.classList.add('nav-active');
            }

            if(document.getElementById('mobile-nav')) {
                document.getElementById('mobile-nav').value = viewId;
            }

            if (viewId === 'quality') {
                initQualityChart();
            }
        }

        const architectureData = {
            presentation: {
                title: "Capa de Presentación",
                desc: "Representada por la interfaz <strong>DentalTimeGUI</strong>. Traduce las entradas de usuario, captura eventos y actualiza la vista interactiva mediante enlaces directos a la capa de aplicación. Emplea Tkinter para garantizar portabilidad.",
                color: "bg-teal-600"
            },
            application: {
                title: "Capa de Aplicación",
                desc: "Encapsulada en la clase <strong>Consultorio</strong>, la cual funciona como controlador de estado. Aquí se ejecutan las validaciones lógicas complejas de solapamiento temporal y los algoritmos de ordenación (Timsort).",
                color: "bg-slate-700"
            },
            domain: {
                title: "Capa de Dominio",
                desc: "Contiene las abstracciones fundamentales (<strong>Paciente</strong> y <strong>Turno</strong>) con validaciones de inicialización interna, libres de efectos colaterales de infraestructura. Uso intensivo de tipos nativos como datetime.",
                color: "bg-slate-500"
            }
        };

        function showLayer(layerId) {
            ['presentation', 'application', 'domain'].forEach(l => {
                const btn = document.getElementById('btn-layer-' + l);
                btn.className = "layer-btn text-left p-3 rounded-md bg-slate-200 text-slate-700 hover:bg-slate-300 transition-colors";
            });

            const activeBtn = document.getElementById('btn-layer-' + layerId);
            activeBtn.className = `layer-btn text-left p-3 rounded-md ${architectureData[layerId].color} text-white font-medium transition-colors`;

            const contentDiv = document.getElementById('layer-content');
            contentDiv.innerHTML = `
                <div class="text-center animate-fade-in">
                    <h4 class="text-xl font-bold text-slate-800 mb-3">${architectureData[layerId].title}</h4>
                    <p class="text-slate-600 text-sm leading-relaxed">${architectureData[layerId].desc}</p>
                </div>
            `;
        }

        const entityData = {
            consultorio: {
                title: "Consultorio",
                sub: "Clase contenedora principal (Raíz)",
                attrs: [
                    { name: "nombre", type: "str", desc: "Nombre de la clínica dental." },
                    { name: "lista_turnos", type: "list[Turno]", desc: "Colección cronológica centralizada de citas activas (1 a Muchos)." }
                ]
            },
            turno: {
                title: "Turno",
                sub: "Intervalo temporal reservado",
                attrs: [
                    { name: "paciente", type: "Paciente", desc: "Instancia asociada al paciente." },
                    { name: "fecha_hora", type: "datetime", desc: "Bloque exacto del inicio del turno." },
                    { name: "motivo", type: "str", desc: "Breve descripción médica del tratamiento." },
                    { name: "duracion_minutos", type: "int", desc: "Intervalo del turno (por defecto 30 minutos)." }
                ]
            },
            paciente: {
                title: "Paciente",
                sub: "Entidad base de registro",
                attrs: [
                    { name: "nombre", type: "str", desc: "Nombre y apellido del paciente." },
                    { name: "telefono", type: "str", desc: "Teléfono directo para alertas de turnos." },
                    { name: "identificacion", type: "str", desc: "ID/DNI que valida la unicidad del registro." }
                ]
            }
        };

        function showEntity(entityId) {
            ['consultorio', 'turno', 'paciente'].forEach(e => {
                const btn = document.getElementById('btn-ent-' + e);
                btn.className = "ent-btn px-4 py-2 bg-slate-100 text-slate-600 rounded-full whitespace-nowrap hover:bg-slate-200 transition-colors";
            });

            const activeBtn = document.getElementById('btn-ent-' + entityId);
            activeBtn.className = "ent-btn px-4 py-2 bg-teal-100 text-teal-800 font-bold rounded-full whitespace-nowrap transition-colors";

            const data = entityData[entityId];
            let rows = "";
            data.attrs.forEach(attr => {
                rows += `<tr class="border-b border-slate-200"><td class="p-2 font-mono text-xs">${attr.name}</td><td class="p-2 text-teal-700">${attr.type}</td><td class="p-2">${attr.desc}</td></tr>`;
            });

            document.getElementById('entity-content').innerHTML = `
                <div class="animate-fade-in">
                    <h4 class="text-lg font-bold text-slate-800 mb-1">${data.title}</h4>
                    <p class="text-sm text-slate-500 mb-4 italic">${data.sub}</p>
                    <table class="w-full text-sm text-left">
                        <thead class="bg-slate-200 text-slate-700">
                            <tr><th class="p-2 rounded-tl-md">Atributo</th><th class="p-2">Tipo</th><th class="p-2 rounded-tr-md">Descripción</th></tr>
                        </thead>
                        <tbody>${rows}</tbody>
                    </table>
                </div>
            `;
        }

        const workflows = {
            agendar: {
                title: "Agendar Turno (Validación Segura)",
                desc: "Proceso de validación temporal antes de confirmar y agregar una nueva cita a la agenda.",
                steps: [
                    { actor: "Interfaz (GUI)", action: "Envía datos: paciente, fecha, hora, motivo.", target: "Consultorio", icon: "💻" },
                    { actor: "Consultorio", action: "Inicia ciclo (loop) validando colisiones contra turnos existentes.", target: "Lista de Turnos", icon: "⚙️" },
                    { actor: "Lista de Turnos", action: "Retorna confirmación: Horario Disponible (Sin solapamientos).", target: "Consultorio", icon: "✅" },
                    { actor: "Consultorio", action: "Ejecuta append(nuevo_turno) y sort() para reordenar la agenda.", target: "Lista de Turnos", icon: "📅" }
                ]
            },
            cancelar: {
                title: "Cancelar Turno (Liberación)",
                desc: "Proceso de remoción y liberación de un turno programado de manera segura.",
                steps: [
                    { actor: "Interfaz (GUI)", action: "Envía solicitud de cancelación con ID o Nombre.", target: "Consultorio", icon: "💻" },
                    { actor: "Consultorio", action: "Inicia ciclo (loop) buscando coincidencias case-insensitive.", target: "Lista de Turnos", icon: "🔍" },
                    { actor: "Lista de Turnos", action: "Identifica y retorna el objeto Turno correspondiente.", target: "Consultorio", icon: "👤" },
                    { actor: "Consultorio", action: "Ejecuta remove(turno), eliminando el registro y liberando el bloque.", target: "Lista de Turnos", icon: "🗑️" }
                ]
            }
        };

        let currentWf = 'agendar';
        let currentStepIdx = 0;

        function loadWorkflow(wfId) {
            document.getElementById('btn-wf-agendar').className = "px-6 py-2 rounded-lg bg-slate-200 text-slate-700 font-bold hover:bg-slate-300 transition-colors";
            document.getElementById('btn-wf-cancelar').className = "px-6 py-2 rounded-lg bg-slate-200 text-slate-700 font-bold hover:bg-slate-300 transition-colors";
            
            document.getElementById('btn-wf-' + wfId).className = "px-6 py-2 rounded-lg bg-teal-600 text-white font-bold shadow-md hover:bg-teal-700 transition-colors";

            currentWf = wfId;
            currentStepIdx = 0;
            
            document.getElementById('wf-title').innerText = workflows[wfId].title;
            document.getElementById('wf-desc').innerText = workflows[wfId].desc;
            
            renderWorkflowSteps();
            updateWorkflowControls();
        }

        function renderWorkflowSteps() {
            const container = document.getElementById('wf-step-container');
            const data = workflows[currentWf].steps;
            let html = "";

            data.forEach((step, idx) => {
                const isVisible = idx <= currentStepIdx;
                const opacity = isVisible ? "opacity-100" : "opacity-0 translate-y-4";
                const isCurrent = idx === currentStepIdx;
                const dotColor = isCurrent ? "bg-teal-500 ring-4 ring-teal-100" : (isVisible ? "bg-slate-400" : "bg-slate-200");
                
                html += `
                    <div class="flex items-start step-transition ${opacity}" style="transition-delay: ${isVisible && isCurrent ? '100ms' : '0ms'}">
                        <div class="absolute left-8 w-4 h-4 rounded-full -ml-2 mt-1.5 ${dotColor} z-20 step-transition"></div>
                        <div class="ml-16 bg-white p-4 rounded-lg border ${isCurrent ? 'border-teal-300 shadow-md' : 'border-slate-200'} w-full relative">
                            <div class="flex items-center text-sm font-bold text-slate-500 mb-1">
                                <span class="mr-2 text-lg">${step.icon}</span> ${step.actor} <span class="mx-2">➡</span> ${step.target}
                            </div>
                            <p class="text-slate-800 font-medium">${step.action}</p>
                        </div>
                    </div>
                `;
            });
            container.innerHTML = html;
        }

        function updateWorkflowControls() {
            const totalSteps = workflows[currentWf].steps.length;
            document.getElementById('step-indicator').innerText = `Paso ${currentStepIdx + 1} de ${totalSteps}`;
            document.getElementById('btn-prev-step').disabled = currentStepIdx === 0;
            document.getElementById('btn-next-step').disabled = currentStepIdx === totalSteps - 1;
        }

        function nextStep() {
            if (currentStepIdx < workflows[currentWf].steps.length - 1) {
                currentStepIdx++;
                renderWorkflowSteps();
                updateWorkflowControls();
            }
        }

        function prevStep() {
            if (currentStepIdx > 0) {
                currentStepIdx--;
                renderWorkflowSteps();
                updateWorkflowControls();
            }
        }

        function initQualityChart() {
            if (chartInstance) {
                return;
            }
            const ctx = document.getElementById('qualityChart').getContext('2d');
            chartInstance = new Chart(ctx, {
                type: 'doughnut',
                data: {
                    labels: ['Tests Aprobados (Passed)', 'Tests Fallidos (Failed)'],
                    datasets: [{
                        data: [7, 0],
                        backgroundColor: ['#0d9488', '#e2e8f0'],
                        borderWidth: 0,
                        hoverOffset: 4
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    cutout: '75%',
                    plugins: {
                        legend: {
                            position: 'bottom',
                            labels: {
                                font: { family: "'Segoe UI', sans-serif", size: 12 },
                                color: '#475569'
                            }
                        },
                        tooltip: {
                            backgroundColor: '#1e293b',
                            titleFont: { size: 13 },
                            bodyFont: { size: 13 },
                            padding: 10,
                            displayColors: true
                        }
                    }
                },
                plugins: [{
                    id: 'textCenter',
                    beforeDraw: function(chart) {
                        var width = chart.width,
                            height = chart.height,
                            ctx = chart.ctx;

                        ctx.restore();
                        var fontSize = (height / 114).toFixed(2);
                        ctx.font = "bold " + fontSize + "em sans-serif";
                        ctx.textBaseline = "middle";
                        ctx.fillStyle = "#0f172a";

                        var text = "100%",
                            textX = Math.round((width - ctx.measureText(text).width) / 2),
                            textY = height / 2 - 15;

                        ctx.fillText(text, textX, textY);
                        
                        ctx.font = (fontSize * 0.4) + "em sans-serif";
                        ctx.fillStyle = "#64748b";
                        var text2 = "Cobertura",
                            text2X = Math.round((width - ctx.measureText(text2).width) / 2),
                            text2Y = height / 2 + 10;
                        ctx.fillText(text2, text2X, text2Y);
                        ctx.save();
                    }
                }]
            });
        }

        document.addEventListener('DOMContentLoaded', () => {
            loadWorkflow('agendar');
        });
    </script>
</body>
</html>