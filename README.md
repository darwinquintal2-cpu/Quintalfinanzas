<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Gestor de Finanzas Personales</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
</head>
<body class="bg-slate-100 text-slate-800 font-sans min-h-screen flex flex-col pb-20">

  <!-- Header Superior -->
  <header class="bg-slate-900 text-white px-6 py-4 shadow-md flex items-center justify-between">
    <div class="flex items-center gap-3">
      <div class="bg-indigo-600 p-2 rounded-xl text-white">
        <i class="fa-solid fa-wallet text-lg"></i>
      </div>
      <h1 class="font-bold text-lg tracking-wide">Finanzas</h1>
    </div>
    <div class="text-xs text-slate-400 font-medium bg-slate-800 px-3 py-1 rounded-full">
      v3.2
    </div>
  </header>

  <!-- Contenido Principal -->
  <main class="flex-1 p-4 md:p-8 overflow-y-auto max-w-7xl w-full mx-auto">

    <!-- TAB 1: RESUMEN -->
    <section id="tab-resumen" class="tab-content space-y-6">
      <div class="flex justify-between items-center">
        <div>
          <h2 class="text-2xl font-bold text-slate-900">Resumen</h2>
          <p class="text-sm text-slate-500">Visión general de tus finanzas en tiempo real.</p>
        </div>
        <button onclick="openModal('modal-transaccion')" class="bg-indigo-600 hover:bg-indigo-700 text-white px-4 py-2.5 rounded-lg text-sm font-medium flex items-center gap-2 shadow-sm transition">
          <i class="fa-solid fa-plus"></i> Nuevo Movimiento
        </button>
      </div>

      <!-- Tarjetas de Métricas -->
      <div class="grid grid-cols-1 sm:grid-cols-3 gap-4">
        <div class="bg-white p-5 rounded-xl shadow-sm border border-slate-200">
          <div class="flex justify-between items-center text-slate-500 text-xs font-semibold tracking-wider uppercase">
            <span>Saldo Total</span>
            <i class="fa-solid fa-wallet text-indigo-500 text-base"></i>
          </div>
          <div id="dash-total-balance" class="text-2xl font-bold mt-2">$0.00</div>
        </div>

        <div class="bg-white p-5 rounded-xl shadow-sm border border-slate-200">
          <div class="flex justify-between items-center text-slate-500 text-xs font-semibold tracking-wider uppercase">
            <span>Ingresos (Mes Actual)</span>
            <span class="text-base">💵</span>
          </div>
          <div id="dash-month-income" class="text-2xl font-bold text-emerald-600 mt-2">$0.00</div>
        </div>

        <div class="bg-white p-5 rounded-xl shadow-sm border border-slate-200">
          <div class="flex justify-between items-center text-slate-500 text-xs font-semibold tracking-wider uppercase">
            <span>Gastos (Mes Actual)</span>
            <span class="text-base">💸</span>
          </div>
          <div id="dash-month-expense" class="text-2xl font-bold text-rose-600 mt-2">$0.00</div>
        </div>
      </div>

      <!-- Gráficos y Últimos Movimientos -->
      <div class="grid grid-cols-1 lg:grid-cols-3 gap-6">
        <div class="bg-white p-5 rounded-xl shadow-sm border border-slate-200 lg:col-span-1">
          <h3 class="font-bold text-slate-800 mb-4">Gastos del Mes</h3>
          <div class="relative flex items-center justify-center min-h-[220px]">
            <canvas id="chartCategorias"></canvas>
          </div>
        </div>

        <div class="bg-white p-5 rounded-xl shadow-sm border border-slate-200 lg:col-span-2">
          <div class="flex justify-between items-center mb-4">
            <h3 class="font-bold text-slate-800">Últimos Movimientos</h3>
            <button onclick="switchTab('transacciones')" class="text-xs text-indigo-600 font-semibold hover:underline">Ver todos</button>
          </div>
          <div id="recent-transactions-list" class="divide-y divide-slate-100">
            <!-- Dinámico -->
          </div>
        </div>
      </div>
    </section>

    <!-- TAB 2: CUENTAS -->
    <section id="tab-cuentas" class="tab-content hidden space-y-6">
      <div class="flex justify-between items-center">
        <div>
          <h2 class="text-2xl font-bold text-slate-900">Cuentas Financieras</h2>
          <p class="text-sm text-slate-500">Administra tus bancos, tarjetas y efectivo.</p>
        </div>
        <button onclick="openModal('modal-cuenta')" class="bg-indigo-600 hover:bg-indigo-700 text-white px-4 py-2 rounded-lg text-sm font-medium flex items-center gap-2">
          <i class="fa-solid fa-plus"></i> Nueva Cuenta
        </button>
      </div>

      <div id="accounts-grid" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
        <!-- Dinámico -->
      </div>
    </section>

    <!-- TAB 3: REGISTRO DE INGRESOS Y GASTOS -->
    <section id="tab-transacciones" class="tab-content hidden space-y-6">
      <div class="flex flex-col sm:flex-row justify-between items-start sm:items-center gap-4">
        <div>
          <h2 class="text-2xl font-bold text-slate-900">Ingresos y Gastos</h2>
          <p class="text-sm text-slate-500">Historial de transacciones y registro detallado.</p>
        </div>
        <div class="flex gap-2">
          <button onclick="openModal('modal-gestionar-categorias')" class="bg-slate-200 hover:bg-slate-300 text-slate-800 px-3.5 py-2 rounded-lg text-sm font-medium flex items-center gap-2 transition">
            <i class="fa-solid fa-tags"></i> Editar Categorías
          </button>
          <button onclick="openModal('modal-transaccion')" class="bg-indigo-600 hover:bg-indigo-700 text-white px-4 py-2 rounded-lg text-sm font-medium flex items-center gap-2 shadow-sm transition">
            <i class="fa-solid fa-plus"></i> Registrar Movimiento
          </button>
        </div>
      </div>

      <!-- Filtros y Búsqueda -->
      <div class="bg-white p-4 rounded-xl shadow-sm border border-slate-200 flex flex-wrap gap-3 items-center justify-between">
        <div class="flex flex-wrap gap-3 w-full md:w-auto">
          <select id="filter-type" onchange="renderTransactions()" class="text-sm border border-slate-300 rounded-lg px-3 py-2 bg-white">
            <option value="all">Todos los tipos</option>
            <option value="income">Solo Ingresos 💵</option>
            <option value="expense">Solo Gastos 💸</option>
          </select>
          <select id="filter-account" onchange="renderTransactions()" class="text-sm border border-slate-300 rounded-lg px-3 py-2 bg-white">
            <option value="all">Todas las cuentas</option>
          </select>
        </div>
        <div class="relative w-full md:w-64">
          <i class="fa-solid fa-magnifying-glass absolute left-3 top-2.5 text-slate-400 text-sm"></i>
          <input type="text" id="search-tx" oninput="renderTransactions()" placeholder="Buscar movimiento..." class="w-full text-sm border border-slate-300 rounded-lg pl-9 pr-3 py-2 focus:outline-none focus:border-indigo-500">
        </div>
      </div>

      <!-- Tabla -->
      <div class="bg-white rounded-xl shadow-sm border border-slate-200 overflow-hidden">
        <div class="overflow-x-auto">
          <table class="w-full text-left text-sm text-slate-600">
            <thead class="bg-slate-50 text-slate-700 uppercase text-xs border-b border-slate-200">
              <tr>
                <th class="px-6 py-3">Fecha</th>
                <th class="px-6 py-3">Descripción</th>
                <th class="px-6 py-3">Categoría</th>
                <th class="px-6 py-3">Cuenta</th>
                <th class="px-6 py-3 text-right">Monto</th>
                <th class="px-6 py-3 text-center">Acciones</th>
              </tr>
            </thead>
            <tbody id="transactions-table-body" class="divide-y divide-slate-100">
              <!-- Dinámico -->
            </tbody>
          </table>
        </div>
      </div>
    </section>

    <!-- TAB 4: PRESUPUESTOS -->
    <section id="tab-presupuestos" class="tab-content hidden space-y-6">
      <div class="flex justify-between items-center">
        <div>
          <h2 class="text-2xl font-bold text-slate-900">Presupuestos Mensuales</h2>
          <p class="text-sm text-slate-500">Establece límites de gasto por categoría.</p>
        </div>
        <button onclick="openModal('modal-presupuesto')" class="bg-indigo-600 hover:bg-indigo-700 text-white px-4 py-2 rounded-lg text-sm font-medium flex items-center gap-2">
          <i class="fa-solid fa-plus"></i> Crear Presupuesto
        </button>
      </div>

      <div id="budgets-warning-banner" class="hidden bg-rose-50 border-l-4 border-rose-500 p-4 rounded-r-xl shadow-sm">
        <div class="flex items-center gap-3">
          <i class="fa-solid fa-triangle-exclamation text-rose-500 text-xl"></i>
          <div>
            <h4 class="font-bold text-rose-800 text-sm">¡Atención! Presupuesto Excedido</h4>
            <p id="budgets-warning-text" class="text-xs text-rose-600 mt-0.5">Tienes categorías donde has sobrepasado tu límite mensual este mes.</p>
          </div>
        </div>
      </div>

      <div id="budgets-grid" class="grid grid-cols-1 md:grid-cols-2 gap-6">
        <!-- Dinámico -->
      </div>
    </section>

    <!-- TAB 5: METAS DE AHORRO -->
    <section id="tab-metas" class="tab-content hidden space-y-6">
      <div class="flex justify-between items-center">
        <div>
          <h2 class="text-2xl font-bold text-slate-900">Metas de Ahorro</h2>
          <p class="text-sm text-slate-500">Planifica tus objetivos financieros a futuro.</p>
        </div>
        <button onclick="openModal('modal-meta')" class="bg-indigo-600 hover:bg-indigo-700 text-white px-4 py-2 rounded-lg text-sm font-medium flex items-center gap-2">
          <i class="fa-solid fa-plus"></i> Nueva Meta
        </button>
      </div>

      <div id="goals-grid" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
        <!-- Dinámico -->
      </div>
    </section>

    <!-- TAB 6: REPORTES MENSUALES -->
    <section id="tab-reportes" class="tab-content hidden space-y-6">
      <div class="flex flex-col sm:flex-row justify-between items-start sm:items-center gap-4">
        <div>
          <h2 class="text-2xl font-bold text-slate-900">Reportes Mensuales</h2>
          <p class="text-sm text-slate-500">Histórico de finanzas y análisis detallado por mes.</p>
        </div>
        <div class="flex items-center gap-2">
          <button onclick="exportCSV()" class="bg-emerald-600 hover:bg-emerald-700 text-white px-3.5 py-2 rounded-xl text-xs font-semibold flex items-center gap-2 transition shadow-sm">
            <i class="fa-solid fa-file-csv text-base"></i> Exportar CSV
          </button>
          <div class="flex items-center gap-2 bg-white px-3 py-2 rounded-xl shadow-sm border border-slate-200">
            <label for="select-report-month" class="text-xs font-semibold text-slate-600">Mes:</label>
            <select id="select-report-month" onchange="renderReports()" class="text-sm font-semibold text-indigo-600 bg-transparent focus:outline-none">
              <!-- Dinámico -->
            </select>
          </div>
        </div>
      </div>

      <div class="grid grid-cols-1 sm:grid-cols-3 gap-4">
        <div class="bg-white p-5 rounded-xl shadow-sm border border-slate-200">
          <div class="flex items-center justify-between">
            <p class="text-xs font-semibold uppercase text-slate-400">Ingresos del Período</p>
            <span>💵</span>
          </div>
          <p id="rep-month-income" class="text-2xl font-bold text-emerald-600 mt-1">$0.00</p>
        </div>
        <div class="bg-white p-5 rounded-xl shadow-sm border border-slate-200">
          <div class="flex items-center justify-between">
            <p class="text-xs font-semibold uppercase text-slate-400">Gastos del Período</p>
            <span>💸</span>
          </div>
          <p id="rep-month-expense" class="text-2xl font-bold text-rose-600 mt-1">$0.00</p>
        </div>
        <div class="bg-white p-5 rounded-xl shadow-sm border border-slate-200">
          <p class="text-xs font-semibold uppercase text-slate-400">Balance del Período</p>
          <p id="rep-month-balance" class="text-2xl font-bold text-slate-900 mt-1">$0.00</p>
        </div>
      </div>

      <div class="bg-white p-5 rounded-xl shadow-sm border border-slate-200">
        <div class="flex justify-between items-center mb-4">
          <h3 class="font-bold text-slate-800">Histórico de Ingresos vs Gastos</h3>
          <span class="text-xs text-slate-400">Evolución mensual</span>
        </div>
        <div class="relative h-72">
          <canvas id="chartHistorico"></canvas>
        </div>
      </div>

      <div class="grid grid-cols-1 lg:grid-cols-2 gap-6">
        <div class="bg-white p-5 rounded-xl shadow-sm border border-slate-200">
          <h3 class="font-bold text-slate-800 mb-4">Distribución de Gastos (<span id="rep-selected-month-label">Mes</span>)</h3>
          <div class="relative flex items-center justify-center min-h-[250px]">
            <canvas id="chartReporteCategoria"></canvas>
          </div>
        </div>

        <div class="bg-white p-5 rounded-xl shadow-sm border border-slate-200 flex flex-col">
          <h3 class="font-bold text-slate-800 mb-4">Detalle por Categoría</h3>
          <div id="rep-category-list" class="divide-y divide-slate-100 flex-1 overflow-y-auto max-h-[250px]">
            <!-- Dinámico -->
          </div>
        </div>
      </div>
    </section>

  </main>

  <!-- Navegación Inferior (Bottom Nav Agrupado) -->
  <nav class="fixed bottom-0 left-0 right-0 bg-slate-900 border-t border-slate-800 z-40 px-2 py-1 shadow-lg">
    <div class="max-w-md md:max-w-xl mx-auto flex justify-around items-center relative">
      
      <button onclick="switchTab('resumen')" id="nav-resumen" class="nav-btn flex flex-col items-center justify-center py-1.5 px-3 rounded-lg text-xs font-medium text-indigo-400 transition">
        <i class="fa-solid fa-chart-pie text-base mb-0.5"></i>
        <span>Resumen</span>
      </button>

      <button onclick="switchTab('transacciones')" id="nav-transacciones" class="nav-btn flex flex-col items-center justify-center py-1.5 px-3 rounded-lg text-xs font-medium text-slate-400 hover:text-white transition">
        <i class="fa-solid fa-right-left text-base mb-0.5"></i>
        <span>Movs</span>
      </button>

      <button onclick="switchTab('presupuestos')" id="nav-presupuestos" class="nav-btn flex flex-col items-center justify-center py-1.5 px-3 rounded-lg text-xs font-medium text-slate-400 hover:text-white transition">
        <i class="fa-solid fa-calculator text-base mb-0.5"></i>
        <span>Límites</span>
      </button>

      <!-- Botón Agrupado Desplegable (Cuentas, Metas, Reportes) -->
      <div class="relative">
        <button onclick="toggleMoreMenu(event)" id="nav-more" class="nav-btn flex flex-col items-center justify-center py-1.5 px-3 rounded-lg text-xs font-medium text-slate-400 hover:text-white transition">
          <i class="fa-solid fa-bars text-base mb-0.5"></i>
          <span>Más</span>
        </button>

        <!-- Menú Desplegable Popover -->
        <div id="more-menu" class="hidden absolute bottom-12 right-0 bg-slate-800 border border-slate-700 rounded-xl shadow-xl w-44 py-1.5 z-50 text-slate-200">
          <button onclick="selectMoreTab('cuentas')" id="nav-cuentas" class="w-full text-left px-4 py-2.5 hover:bg-slate-700 text-xs font-medium flex items-center gap-3 transition">
            <i class="fa-solid fa-building-columns text-indigo-400 w-4"></i>
            <span>Cuentas</span>
          </button>
          <button onclick="selectMoreTab('metas')" id="nav-metas" class="w-full text-left px-4 py-2.5 hover:bg-slate-700 text-xs font-medium flex items-center gap-3 transition">
            <i class="fa-solid fa-bullseye text-indigo-400 w-4"></i>
            <span>Metas</span>
          </button>
          <button onclick="selectMoreTab('reportes')" id="nav-reportes" class="w-full text-left px-4 py-2.5 hover:bg-slate-700 text-xs font-medium flex items-center gap-3 transition">
            <i class="fa-solid fa-chart-column text-indigo-400 w-4"></i>
            <span>Reportes</span>
          </button>
        </div>
      </div>

    </div>
  </nav>

  <!-- MODALES -->

  <!-- Modal: Aporte o Retiro de Meta -->
  <div id="modal-aporte-meta" class="fixed inset-0 bg-slate-900/60 hidden items-center justify-center p-4 z-50">
    <div class="bg-white rounded-2xl shadow-xl max-w-sm w-full p-6 space-y-4">
      <div class="flex justify-between items-center">
        <h3 id="goal-modal-title" class="font-bold text-lg text-slate-800">Modificar Ahorro</h3>
        <button onclick="closeModal('modal-aporte-meta')" class="text-slate-400 hover:text-slate-600"><i class="fa-solid fa-xmark"></i></button>
      </div>
      <form id="form-aporte-meta" onsubmit="saveGoalContribution(event)" class="space-y-3">
        <input type="hidden" id="goal-deposit-id">
        <div>
          <label class="text-xs font-semibold text-slate-600">Tipo de Operación</label>
          <select id="goal-action-type" class="w-full mt-1 border border-slate-300 rounded-lg p-2 text-sm font-semibold">
            <option value="deposit">Abonar (+)</option>
            <option value="withdraw">Retirar (-)</option>
          </select>
        </div>
        <div>
          <label class="text-xs font-semibold text-slate-600">Monto</label>
          <input type="number" step="0.01" id="goal-deposit-amount" required class="w-full mt-1 border border-slate-300 rounded-lg p-2 text-sm" placeholder="0.00">
        </div>
        <div class="flex justify-end gap-2 pt-2">
          <button type="button" onclick="closeModal('modal-aporte-meta')" class="px-4 py-2 text-sm text-slate-600 bg-slate-100 rounded-lg">Cancelar</button>
          <button type="submit" class="px-4 py-2 text-sm text-white bg-indigo-600 rounded-lg font-medium">Confirmar</button>
        </div>
      </form>
    </div>
  </div>

  <!-- Modal: Alerta de Presupuesto Excedido -->
  <div id="modal-alerta-presupuesto" class="fixed inset-0 bg-slate-900/60 hidden items-center justify-center p-4 z-50">
    <div class="bg-white rounded-2xl shadow-2xl max-w-md w-full p-6 text-center space-y-4 border-2 border-rose-500">
      <div class="w-16 h-16 bg-rose-100 text-rose-600 rounded-full flex items-center justify-center mx-auto text-3xl">
        <i class="fa-solid fa-triangle-exclamation"></i>
      </div>
      <div>
        <h3 class="font-bold text-xl text-slate-900">¡Presupuesto Excedido!</h3>
        <p class="text-xs text-slate-500 mt-1" id="alert-budget-msg">Has sobrepasado el límite mensual establecido.</p>
      </div>
      <div class="bg-rose-50/80 p-4 rounded-xl text-left text-sm space-y-2 border border-rose-100">
        <div class="flex justify-between font-semibold text-slate-700">
          <span>Categoría:</span>
          <span id="alert-budget-cat" class="text-slate-900 font-bold">--</span>
        </div>
        <div class="flex justify-between text-slate-600">
          <span>Límite Mensual:</span>
          <span id="alert-budget-limit" class="font-bold text-slate-800">$0.00</span>
        </div>
        <div class="flex justify-between text-slate-600">
          <span>Gastado este mes:</span>
          <span id="alert-budget-spent" class="font-bold text-rose-600">$0.00</span>
        </div>
        <div class="flex justify-between text-xs pt-2 border-t border-rose-200 text-rose-700 font-bold">
          <span>Monto Excedido:</span>
          <span id="alert-budget-over" class="text-sm">$0.00</span>
        </div>
      </div>
      <button onclick="closeModal('modal-alerta-presupuesto')" class="w-full bg-rose-600 hover:bg-rose-700 text-white font-semibold py-2.5 rounded-xl shadow-md transition">
        Entendido
      </button>
    </div>
  </div>

  <!-- Modal: Crear / Editar Transacción -->
  <div id="modal-transaccion" class="fixed inset-0 bg-slate-900/50 hidden items-center justify-center p-4 z-50">
    <div class="bg-white rounded-xl shadow-xl max-w-md w-full p-6 space-y-4">
      <div class="flex justify-between items-center">
        <h3 id="modal-tx-title" class="font-bold text-lg text-slate-800">Registrar Movimiento</h3>
        <button onclick="closeModal('modal-transaccion')" class="text-slate-400 hover:text-slate-600"><i class="fa-solid fa-xmark"></i></button>
      </div>
      <form id="form-transaccion" onsubmit="addTransaction(event)" class="space-y-3">
        <input type="hidden" id="tx-edit-id" value="">

        <div>
          <label class="text-xs font-semibold text-slate-600">Tipo de Movimiento</label>
          <select id="tx-type" onchange="updateTxCategoryDropdown()" class="w-full mt-1 border border-slate-300 rounded-lg p-2 text-sm font-semibold">
            <option value="expense">Gasto 💸</option>
            <option value="income">Ingreso 💵</option>
          </select>
        </div>
        <div>
          <label class="text-xs font-semibold text-slate-600">Monto</label>
          <input type="number" step="0.01" id="tx-amount" required class="w-full mt-1 border border-slate-300 rounded-lg p-2 text-sm" placeholder="0.00">
        </div>
        <div>
          <label class="text-xs font-semibold text-slate-600">Descripción</label>
          <input type="text" id="tx-desc" required class="w-full mt-1 border border-slate-300 rounded-lg p-2 text-sm" placeholder="Ej. Supermercado, Honorarios">
        </div>
        <div>
          <label class="text-xs font-semibold text-slate-600">Categoría</label>
          <select id="tx-category" class="w-full mt-1 border border-slate-300 rounded-lg p-2 text-sm">
            <!-- Dinámico -->
          </select>
        </div>
        <div>
          <label class="text-xs font-semibold text-slate-600">Cuenta</label>
          <select id="tx-account" class="w-full mt-1 border border-slate-300 rounded-lg p-2 text-sm"></select>
        </div>
        <div>
          <label class="text-xs font-semibold text-slate-600">Fecha</label>
          <input type="date" id="tx-date" required class="w-full mt-1 border border-slate-300 rounded-lg p-2 text-sm">
        </div>
        <div class="flex justify-end gap-2 pt-3">
          <button type="button" onclick="closeModal('modal-transaccion')" class="px-4 py-2 text-sm text-slate-600 bg-slate-100 rounded-lg">Cancelar</button>
          <button type="submit" class="px-4 py-2 text-sm text-white bg-indigo-600 rounded-lg">Guardar</button>
        </div>
      </form>
    </div>
  </div>

  <!-- Modal: Gestionar Categorías -->
  <div id="modal-gestionar-categorias" class="fixed inset-0 bg-slate-900/50 hidden items-center justify-center p-4 z-50">
    <div class="bg-white rounded-xl shadow-xl max-w-md w-full p-6 space-y-4">
      <div class="flex justify-between items-center">
        <h3 class="font-bold text-lg text-slate-800">Gestionar Categorías</h3>
        <button onclick="closeModal('modal-gestionar-categorias')" class="text-slate-400 hover:text-slate-600"><i class="fa-solid fa-xmark"></i></button>
      </div>

      <form id="form-nueva-categoria" onsubmit="saveCategory(event)" class="bg-slate-50 p-3.5 rounded-xl border border-slate-200 space-y-3">
        <p class="text-xs font-bold text-slate-700">Añadir o Editar Categoría</p>
        
        <div class="grid grid-cols-12 gap-2">
          <div class="col-span-3">
            <label class="text-[10px] font-semibold text-slate-500 block mb-0.5">Icono</label>
            <input type="text" id="cat-icon-input" oninput="renderEmojiPicker()" required maxlength="4" placeholder="Emoji" class="w-full border border-slate-300 rounded-lg p-2 text-center text-sm font-bold bg-white">
          </div>
          <div class="col-span-9">
            <label class="text-[10px] font-semibold text-slate-500 block mb-0.5">Nombre Categoría</label>
            <input type="text" id="cat-name-input" required placeholder="Ej. Restaurantes" class="w-full border border-slate-300 rounded-lg p-2 text-sm bg-white">
          </div>
        </div>

        <div>
          <label class="text-[10px] font-semibold text-slate-500 block mb-1">Selecciona un emoji disponible:</label>
          <div id="emoji-picker-container" class="grid grid-cols-7 gap-1.5 max-h-32 overflow-y-auto bg-white p-2 rounded-lg border border-slate-200">
            <!-- Dinámico -->
          </div>
        </div>

        <div class="flex gap-2 pt-1">
          <select id="cat-type-input" class="flex-1 border border-slate-300 rounded-lg p-2 text-xs bg-white font-medium">
            <option value="expense">Para Gastos 💸</option>
            <option value="income">Para Ingresos 💵</option>
            <option value="both">Para Ambos</option>
          </select>
          <button type="submit" class="bg-indigo-600 text-white px-4 py-2 rounded-lg text-xs font-medium hover:bg-indigo-700 transition">Guardar</button>
        </div>
      </form>

      <div class="space-y-1">
        <p class="text-xs font-semibold text-slate-500 mb-1">Categorías Registradas:</p>
        <div id="categories-manager-list" class="max-h-40 overflow-y-auto divide-y divide-slate-100 border border-slate-200 rounded-xl px-2 bg-white">
          <!-- Dinámico -->
        </div>
      </div>

      <div class="flex justify-end pt-2">
        <button type="button" onclick="closeModal('modal-gestionar-categorias')" class="px-4 py-2 text-sm text-white bg-slate-800 rounded-lg">Cerrar</button>
      </div>
    </div>
  </div>

  <!-- Modal: Nueva Cuenta -->
  <div id="modal-cuenta" class="fixed inset-0 bg-slate-900/50 hidden items-center justify-center p-4 z-50">
    <div class="bg-white rounded-xl shadow-xl max-w-md w-full p-6 space-y-4">
      <div class="flex justify-between items-center">
        <h3 class="font-bold text-lg text-slate-800">Agregar Nueva Cuenta</h3>
        <button onclick="closeModal('modal-cuenta')" class="text-slate-400 hover:text-slate-600"><i class="fa-solid fa-xmark"></i></button>
      </div>
      <form id="form-cuenta" onsubmit="addAccount(event)" class="space-y-3">
        <div>
          <label class="text-xs font-semibold text-slate-600">Nombre de la cuenta</label>
          <input type="text" id="acc-name" required class="w-full mt-1 border border-slate-300 rounded-lg p-2 text-sm" placeholder="Ej. BBVA, Efectivo">
        </div>
        <div>
          <label class="text-xs font-semibold text-slate-600">Tipo</label>
          <select id="acc-type" class="w-full mt-1 border border-slate-300 rounded-lg p-2 text-sm">
            <option value="Banco">Banco</option>
            <option value="Efectivo">Efectivo</option>
            <option value="Tarjeta de Crédito">Tarjeta de Crédito</option>
            <option value="Inversión">Inversión</option>
          </select>
        </div>
        <div>
          <label class="text-xs font-semibold text-slate-600">Saldo Inicial</label>
          <input type="number" step="0.01" id="acc-balance" required class="w-full mt-1 border border-slate-300 rounded-lg p-2 text-sm" placeholder="0.00">
        </div>
        <div class="flex justify-end gap-2 pt-3">
          <button type="button" onclick="closeModal('modal-cuenta')" class="px-4 py-2 text-sm text-slate-600 bg-slate-100 rounded-lg">Cancelar</button>
          <button type="submit" class="px-4 py-2 text-sm text-white bg-indigo-600 rounded-lg">Guardar</button>
        </div>
      </form>
    </div>
  </div>

  <!-- Modal: Nuevo Presupuesto -->
  <div id="modal-presupuesto" class="fixed inset-0 bg-slate-900/50 hidden items-center justify-center p-4 z-50">
    <div class="bg-white rounded-xl shadow-xl max-w-md w-full p-6 space-y-4">
      <div class="flex justify-between items-center">
        <h3 class="font-bold text-lg text-slate-800">Establecer Presupuesto</h3>
        <button onclick="closeModal('modal-presupuesto')" class="text-slate-400 hover:text-slate-600"><i class="fa-solid fa-xmark"></i></button>
      </div>
      <form id="form-presupuesto" onsubmit="addBudget(event)" class="space-y-3">
        <div>
          <label class="text-xs font-semibold text-slate-600">Categoría de Gasto</label>
          <select id="bg-category" class="w-full mt-1 border border-slate-300 rounded-lg p-2 text-sm">
            <!-- Dinámico -->
          </select>
        </div>
        <div>
          <label class="text-xs font-semibold text-slate-600">Límite Mensual</label>
          <input type="number" step="0.01" id="bg-limit" required class="w-full mt-1 border border-slate-300 rounded-lg p-2 text-sm" placeholder="0.00">
        </div>
        <div class="flex justify-end gap-2 pt-3">
          <button type="button" onclick="closeModal('modal-presupuesto')" class="px-4 py-2 text-sm text-slate-600 bg-slate-100 rounded-lg">Cancelar</button>
          <button type="submit" class="px-4 py-2 text-sm text-white bg-indigo-600 rounded-lg">Guardar</button>
        </div>
      </form>
    </div>
  </div>

  <!-- Modal: Nueva Meta -->
  <div id="modal-meta" class="fixed inset-0 bg-slate-900/50 hidden items-center justify-center p-4 z-50">
    <div class="bg-white rounded-xl shadow-xl max-w-md w-full p-6 space-y-4">
      <div class="flex justify-between items-center">
        <h3 class="font-bold text-lg text-slate-800">Nueva Meta de Ahorro</h3>
        <button onclick="closeModal('modal-meta')" class="text-slate-400 hover:text-slate-600"><i class="fa-solid fa-xmark"></i></button>
      </div>
      <form id="form-meta" onsubmit="addGoal(event)" class="space-y-3">
        <div>
          <label class="text-xs font-semibold text-slate-600">Nombre de la Meta</label>
          <input type="text" id="gl-name" required class="w-full mt-1 border border-slate-300 rounded-lg p-2 text-sm" placeholder="Ej. Fondo de Emergencia, Vacaciones">
        </div>
        <div>
          <label class="text-xs font-semibold text-slate-600">Monto Objetivo</label>
          <input type="number" step="0.01" id="gl-target" required class="w-full mt-1 border border-slate-300 rounded-lg p-2 text-sm" placeholder="0.00">
        </div>
        <div>
          <label class="text-xs font-semibold text-slate-600">Monto Inicial Ahorrado</label>
          <input type="number" step="0.01" id="gl-current" value="0" class="w-full mt-1 border border-slate-300 rounded-lg p-2 text-sm">
        </div>
        <div class="flex justify-end gap-2 pt-3">
          <button type="button" onclick="closeModal('modal-meta')" class="px-4 py-2 text-sm text-slate-600 bg-slate-100 rounded-lg">Cancelar</button>
          <button type="submit" class="px-4 py-2 text-sm text-white bg-indigo-600 rounded-lg">Guardar</button>
        </div>
      </form>
    </div>
  </div>

  <!-- LÓGICA JAVASCRIPT -->
  <script>
    const emojiList = [
      '🍔', '🍕', '☕', '🛒', '🏠', '💡', '🚗', '⛽', '🚌', '✈️', 
      '🎮', '🎬', '🍿', '👕', '🩺', '🏥', '💳', '💰', '💵', '🏦', 
      '📈', '💼', '🎁', '📱', '🏋️', '🐾', '🎓', '🏖️', '👨‍👩‍👧‍‍👦', '📦', 
      '🔧', '🎨', '🎵', '⚽', '💻'
    ];

    const defaultCategories = [
      { name: 'Alimentación', icon: '🍔', type: 'expense' },
      { name: 'Vivienda', icon: '🏠', type: 'expense' },
      { name: 'Servicios', icon: '💡', type: 'expense' },
      { name: 'Entretenimiento', icon: '🎮', type: 'expense' },
      { name: 'Transporte', icon: '🚗', type: 'expense' },
      { name: 'Familia', icon: '👨‍👩‍👧‍👦', type: 'both' },
      { name: 'Salud', icon: '🩺', type: 'expense' },
      { name: 'Deuda', icon: '💳', type: 'expense' },
      { name: 'Nómina', icon: '💰', type: 'income' },
      { name: 'Ventas', icon: '📈', type: 'income' },
      { name: 'Otros', icon: '📦', type: 'both' }
    ];

    const initialData = {
      categories: defaultCategories,
      accounts: [
        { id: 'acc_1', name: 'Cuenta Principal', type: 'Banco', balance: 34800 },
        { id: 'acc_2', name: 'Efectivo', type: 'Efectivo', balance: 2500 }
      ],
      transactions: [
        { id: 'tx_s1', type: 'income', amount: 32000, category: 'Nómina', accountId: 'acc_1', date: '2026-09-01', description: 'Sueldo Septiembre' },
        { id: 'tx_s2', type: 'expense', amount: 12000, category: 'Vivienda', accountId: 'acc_1', date: '2026-09-05', description: 'Renta' },
        { id: 'tx_s3', type: 'expense', amount: 2500, category: 'Familia', accountId: 'acc_1', date: '2026-09-08', description: 'Gastos Escolares' },
        { id: 'tx_s4', type: 'expense', amount: 1800, category: 'Salud', accountId: 'acc_1', date: '2026-09-12', description: 'Medicamentos' },
        { id: 'tx_s5', type: 'expense', amount: 3000, category: 'Deuda', accountId: 'acc_1', date: '2026-09-15', description: 'Pago Tarjeta' }
      ],
      budgets: [
        { id: 'b_1', category: 'Alimentación', limit: 8000 },
        { id: 'b_2', category: 'Familia', limit: 5000 },
        { id: 'b_3', category: 'Salud', limit: 3000 }
      ],
      goals: [
        { id: 'g_1', name: 'Fondo de Emergencia', targetAmount: 50000, currentAmount: 20000 }
      ]
    };

    let state = JSON.parse(localStorage.getItem('finanzas_data')) || initialData;
    
    if (!state.categories) {
      state.categories = defaultCategories;
    } else {
      state.categories.forEach(c => { if (!c.type) c.type = 'both'; });
    }

    function saveData() {
      localStorage.setItem('finanzas_data', JSON.stringify(state));
      renderAll();
    }

    let chartCatInstance = null;
    let chartHistInstance = null;
    let chartRepCatInstance = null;

    document.addEventListener('DOMContentLoaded', () => {
      document.getElementById('tx-date').value = new Date().toISOString().split('T')[0];
      renderAll();

      // Cerrar menú "Más" al hacer clic fuera
      document.addEventListener('click', (e) => {
        const moreMenu = document.getElementById('more-menu');
        const navMoreBtn = document.getElementById('nav-more');
        if (moreMenu && !moreMenu.classList.contains('hidden')) {
          if (!moreMenu.contains(e.target) && !navMoreBtn.contains(e.target)) {
            moreMenu.classList.add('hidden');
          }
        }
      });
    });

    function formatCurrency(amount) {
      return new Intl.NumberFormat('es-MX', { style: 'currency', currency: 'MXN' }).format(amount);
    }

    function getCategoryIcon(catName) {
      const found = state.categories.find(c => c.name.toLowerCase() === catName.toLowerCase());
      return found ? found.icon : '📦';
    }

    function getAccountIcon(accType) {
      switch(accType) {
        case 'Banco': return 'fa-building-columns';
        case 'Efectivo': return 'fa-money-bill-wave';
        case 'Tarjeta de Crédito': return 'fa-credit-card';
        case 'Inversión': return 'fa-chart-line';
        default: return 'fa-wallet';
      }
    }

    function getMonthName(yearMonthStr) {
      if (!yearMonthStr || yearMonthStr === 'all') return 'Todo el Histórico';
      const [year, month] = yearMonthStr.split('-');
      const date = new Date(parseInt(year), parseInt(month) - 1, 1);
      const name = date.toLocaleString('es-ES', { month: 'long' });
      return name.charAt(0).toUpperCase() + name.slice(1) + ' ' + year;
    }

    // GESTIÓN DEL MENÚ DESPLEGABLE "MÁS"
    function toggleMoreMenu(event) {
      event.stopPropagation();
      const menu = document.getElementById('more-menu');
      menu.classList.toggle('hidden');
    }

    function selectMoreTab(tabId) {
      document.getElementById('more-menu').classList.add('hidden');
      switchTab(tabId);
    }

    function switchTab(tabId) {
      document.querySelectorAll('.tab-content').forEach(el => el.classList.add('hidden'));
      document.getElementById(`tab-${tabId}`).classList.remove('hidden');

      // Restablecer estilos de navegación
      document.querySelectorAll('.nav-btn').forEach(btn => {
        btn.classList.remove('text-indigo-400');
        btn.classList.add('text-slate-400');
      });

      // Si la pestaña elegida es Cuentas, Metas o Reportes, marcar botón "Más" como activo
      if (['cuentas', 'metas', 'reportes'].includes(tabId)) {
        const moreBtn = document.getElementById('nav-more');
        if (moreBtn) {
          moreBtn.classList.add('text-indigo-400');
          moreBtn.classList.remove('text-slate-400');
        }
      } else {
        const activeBtn = document.getElementById(`nav-${tabId}`);
        if (activeBtn) {
          activeBtn.classList.add('text-indigo-400');
          activeBtn.classList.remove('text-slate-400');
        }
      }

      if (tabId === 'resumen') renderDashboard();
      if (tabId === 'presupuestos') renderBudgets();
      if (tabId === 'reportes') renderReports();
    }

    function openModal(modalId) {
      document.getElementById(modalId).classList.remove('hidden');
      document.getElementById(modalId).classList.add('flex');
      
      if (modalId === 'modal-transaccion') {
        const editId = document.getElementById('tx-edit-id').value;
        if (!editId) {
          document.getElementById('modal-tx-title').textContent = 'Registrar Movimiento';
          document.getElementById('form-transaccion').reset();
          document.getElementById('tx-date').value = new Date().toISOString().split('T')[0];
          updateTxCategoryDropdown();
        }
      }
      if (modalId === 'modal-gestionar-categorias') {
        renderEmojiPicker();
      }
    }

    function closeModal(modalId) {
      document.getElementById(modalId).classList.add('hidden');
      document.getElementById(modalId).classList.remove('flex');

      if (modalId === 'modal-transaccion') {
        document.getElementById('tx-edit-id').value = '';
        document.getElementById('form-transaccion').reset();
      }
    }

    function renderAll() {
      populateAccountDropdowns();
      populateCategoryDropdowns();
      renderCategoryManagerList();
      renderEmojiPicker();
      renderDashboard();
      renderAccounts();
      renderTransactions();
      renderBudgets();
      renderGoals();
      renderReports();
    }

    function populateAccountDropdowns() {
      const selectTx = document.getElementById('tx-account');
      const selectFilter = document.getElementById('filter-account');
      selectTx.innerHTML = '';
      selectFilter.innerHTML = '<option value="all">Todas las cuentas</option>';

      state.accounts.forEach(acc => {
        selectTx.innerHTML += `<option value="${acc.id}">${acc.name}</option>`;
        selectFilter.innerHTML += `<option value="${acc.id}">${acc.name}</option>`;
      });
    }

    function renderEmojiPicker() {
      const container = document.getElementById('emoji-picker-container');
      if (!container) return;
      container.innerHTML = '';

      const currentSelectedIcon = document.getElementById('cat-icon-input').value.trim();

      emojiList.forEach(emoji => {
        const isSelected = emoji === currentSelectedIcon;
        const btn = document.createElement('button');
        btn.type = 'button';
        btn.className = `h-8 w-8 text-base rounded-lg flex items-center justify-center transition border ${
          isSelected 
            ? 'bg-indigo-100 border-indigo-600 scale-110 shadow-sm' 
            : 'bg-slate-50 border-slate-200 hover:bg-slate-100 hover:border-slate-300'
        }`;
        btn.textContent = emoji;
        btn.onclick = () => selectEmoji(emoji);
        container.appendChild(btn);
      });
    }

    function selectEmoji(emoji) {
      document.getElementById('cat-icon-input').value = emoji;
      renderEmojiPicker();
    }

    function updateTxCategoryDropdown() {
      const selectedType = document.getElementById('tx-type').value;
      const selectTxCat = document.getElementById('tx-category');
      selectTxCat.innerHTML = '';

      const filtered = state.categories.filter(c => c.type === selectedType || c.type === 'both');

      if (filtered.length === 0) {
        selectTxCat.innerHTML = '<option value="">Sin categorías disponibles</option>';
      } else {
        filtered.forEach(c => {
          selectTxCat.innerHTML += `<option value="${c.name}">${c.icon} ${c.name}</option>`;
        });
      }
    }

    function populateCategoryDropdowns() {
      updateTxCategoryDropdown();

      const selectBgCat = document.getElementById('bg-category');
      if (selectBgCat) {
        selectBgCat.innerHTML = '';
        const bgCategories = state.categories.filter(c => c.type === 'expense' || c.type === 'both');
        bgCategories.forEach(c => {
          selectBgCat.innerHTML += `<option value="${c.name}">${c.icon} ${c.name}</option>`;
        });
      }
    }

    function renderCategoryManagerList() {
      const listContainer = document.getElementById('categories-manager-list');
      if (!listContainer) return;
      listContainer.innerHTML = '';

      state.categories.forEach((cat, index) => {
        let badgeColor = 'bg-indigo-100 text-indigo-700';
        let badgeText = 'Ambos';

        if (cat.type === 'expense') {
          badgeColor = 'bg-rose-100 text-rose-700';
          badgeText = 'Gasto 💸';
        } else if (cat.type === 'income') {
          badgeColor = 'bg-emerald-100 text-emerald-700';
          badgeText = 'Ingreso 💵';
        }

        listContainer.innerHTML += `
          <div class="flex justify-between items-center py-2 px-1">
            <div class="flex items-center gap-2">
              <span class="text-sm font-medium text-slate-800">${cat.icon} ${cat.name}</span>
              <span class="text-[10px] font-bold px-2 py-0.5 rounded-full ${badgeColor}">${badgeText}</span>
            </div>
            <div class="flex gap-2">
              <button onclick="editCategory('${cat.name}', '${cat.icon}', '${cat.type}')" class="text-xs text-indigo-600 hover:underline"><i class="fa-solid fa-pen"></i></button>
              <button onclick="deleteCategory(${index})" class="text-xs text-rose-500 hover:underline"><i class="fa-solid fa-trash"></i></button>
            </div>
          </div>
        `;
      });
    }

    function saveCategory(e) {
      e.preventDefault();
      const icon = document.getElementById('cat-icon-input').value.trim();
      const name = document.getElementById('cat-name-input').value.trim();
      const type = document.getElementById('cat-type-input').value;

      if (!name || !icon) return;

      const existingIndex = state.categories.findIndex(c => c.name.toLowerCase() === name.toLowerCase());
      if (existingIndex >= 0) {
        state.categories[existingIndex] = { name, icon, type };
      } else {
        state.categories.push({ name, icon, type });
      }

      saveData();
      e.target.reset();
      renderEmojiPicker();
    }

    function editCategory(name, icon, type) {
      document.getElementById('cat-name-input').value = name;
      document.getElementById('cat-icon-input').value = icon;
      document.getElementById('cat-type-input').value = type || 'both';
      renderEmojiPicker();
    }

    function deleteCategory(index) {
      if (state.categories.length <= 1) {
        alert("Debes conservar al menos una categoría.");
        return;
      }
      state.categories.splice(index, 1);
      saveData();
    }

    // RESUMEN
    function renderDashboard() {
      const totalBalance = state.accounts.reduce((acc, a) => acc + parseFloat(a.balance), 0);
      
      const now = new Date();
      const currentMonth = now.getMonth();
      const currentYear = now.getFullYear();

      const monthTx = state.transactions.filter(t => {
        const d = new Date(t.date);
        return d.getMonth() === currentMonth && d.getFullYear() === currentYear;
      });

      const monthIncome = monthTx.filter(t => t.type === 'income').reduce((acc, t) => acc + parseFloat(t.amount), 0);
      const monthExpense = monthTx.filter(t => t.type === 'expense').reduce((acc, t) => acc + parseFloat(t.amount), 0);

      const totalBalanceEl = document.getElementById('dash-total-balance');
      totalBalanceEl.textContent = formatCurrency(totalBalance);

      if (monthExpense > monthIncome || totalBalance < 0) {
        totalBalanceEl.className = "text-2xl font-bold text-rose-600 mt-2";
      } else {
        totalBalanceEl.className = "text-2xl font-bold text-slate-900 mt-2";
      }

      document.getElementById('dash-month-income').textContent = formatCurrency(monthIncome);
      document.getElementById('dash-month-expense').textContent = formatCurrency(monthExpense);

      const recentList = document.getElementById('recent-transactions-list');
      recentList.innerHTML = '';
      const recent = [...state.transactions].reverse().slice(0, 5);

      if (recent.length === 0) {
        recentList.innerHTML = '<p class="text-xs text-slate-400 py-4 text-center">No hay movimientos registrados.</p>';
      } else {
        recent.forEach(t => {
          const acc = state.accounts.find(a => a.id === t.accountId);
          const isIncome = t.type === 'income';
          const icon = getCategoryIcon(t.category);
          recentList.innerHTML += `
            <div class="py-3 flex items-center justify-between">
              <div class="flex items-center gap-3">
                <div class="w-9 h-9 rounded-full ${isIncome ? 'bg-emerald-100 text-emerald-600' : 'bg-rose-100 text-rose-600'} flex items-center justify-center text-sm font-bold">
                  ${icon}
                </div>
                <div>
                  <p class="text-sm font-semibold text-slate-800">${t.description}</p>
                  <p class="text-xs text-slate-400">${t.category} • ${acc ? acc.name : 'N/A'}</p>
                </div>
              </div>
              <div class="text-right">
                <p class="text-sm font-bold ${isIncome ? 'text-emerald-600' : 'text-rose-600'}">
                  ${isIncome ? '+' : '-'}${formatCurrency(t.amount)}
                </p>
                <p class="text-xs text-slate-400">${t.date}</p>
              </div>
            </div>
          `;
        });
      }

      const expByCat = {};
      monthTx.filter(t => t.type === 'expense').forEach(t => {
        expByCat[t.category] = (expByCat[t.category] || 0) + parseFloat(t.amount);
      });

      const ctxCat = document.getElementById('chartCategorias').getContext('2d');
      if (chartCatInstance) chartCatInstance.destroy();

      const labelsWithIcons = Object.keys(expByCat).map(c => `${getCategoryIcon(c)} ${c}`);

      chartCatInstance = new Chart(ctxCat, {
        type: 'doughnut',
        data: {
          labels: labelsWithIcons.length ? labelsWithIcons : ['Sin Gastos'],
          datasets: [{
            data: Object.values(expByCat).length ? Object.values(expByCat) : [1],
            backgroundColor: Object.values(expByCat).length ? ['#f43f5e', '#6366f1', '#06b6d4', '#f59e0b', '#10b981', '#8b5cf6', '#ec4899'] : ['#e2e8f0']
          }]
        },
        options: { responsive: true, maintainAspectRatio: false, plugins: { legend: { position: 'bottom' } } }
      });
    }

    // CUENTAS
    function renderAccounts() {
      const grid = document.getElementById('accounts-grid');
      grid.innerHTML = '';
      state.accounts.forEach(a => {
        const iconClass = getAccountIcon(a.type);
        grid.innerHTML += `
          <div class="bg-white p-5 rounded-xl shadow-sm border border-slate-200 flex justify-between items-center">
            <div class="flex items-center gap-4">
              <div class="w-12 h-12 rounded-xl bg-indigo-50 text-indigo-600 flex items-center justify-center text-xl">
                <i class="fa-solid ${iconClass}"></i>
              </div>
              <div>
                <span class="text-xs font-semibold uppercase text-indigo-600 tracking-wider">${a.type}</span>
                <h3 class="text-lg font-bold text-slate-800 mt-0.5">${a.name}</h3>
                <p class="text-xl font-bold text-slate-900 mt-1">${formatCurrency(a.balance)}</p>
              </div>
            </div>
            <button onclick="deleteAccount('${a.id}')" class="text-slate-300 hover:text-rose-500 transition p-2"><i class="fa-solid fa-trash"></i></button>
          </div>
        `;
      });
    }

    // TRANSACCIONES
    function renderTransactions() {
      const tbody = document.getElementById('transactions-table-body');
      tbody.innerHTML = '';

      const typeFilter = document.getElementById('filter-type').value;
      const accFilter = document.getElementById('filter-account').value;
      const query = document.getElementById('search-tx').value.toLowerCase().trim();

      let filtered = [...state.transactions].reverse();
      if (typeFilter !== 'all') filtered = filtered.filter(t => t.type === typeFilter);
      if (accFilter !== 'all') filtered = filtered.filter(t => t.accountId === accFilter);
      if (query) {
        filtered = filtered.filter(t => 
          t.description.toLowerCase().includes(query) || 
          t.category.toLowerCase().includes(query)
        );
      }

      if (filtered.length === 0) {
        tbody.innerHTML = `<tr><td colspan="6" class="px-6 py-8 text-center text-slate-400">No se encontraron movimientos.</td></tr>`;
        return;
      }

      filtered.forEach(t => {
        const acc = state.accounts.find(a => a.id === t.accountId);
        const isIncome = t.type === 'income';
        const icon = getCategoryIcon(t.category);
        tbody.innerHTML += `
          <tr class="hover:bg-slate-50">
            <td class="px-6 py-4 whitespace-nowrap text-xs text-slate-500">${t.date}</td>
            <td class="px-6 py-4 font-semibold text-slate-800">${t.description}</td>
            <td class="px-6 py-4"><span class="bg-slate-100 text-slate-700 text-xs px-2.5 py-1 rounded-full font-medium">${icon} ${t.category}</span></td>
            <td class="px-6 py-4 text-xs text-slate-500">${acc ? acc.name : 'Desconocida'}</td>
            <td class="px-6 py-4 text-right font-bold ${isIncome ? 'text-emerald-600' : 'text-rose-600'}">
              ${isIncome ? '+' : '-'}${formatCurrency(t.amount)}
            </td>
            <td class="px-6 py-4 text-center">
              <button onclick="editTransaction('${t.id}')" class="text-slate-400 hover:text-indigo-600 mr-3" title="Editar"><i class="fa-solid fa-pen"></i></button>
              <button onclick="deleteTransaction('${t.id}')" class="text-slate-400 hover:text-rose-600" title="Eliminar"><i class="fa-solid fa-trash"></i></button>
            </td>
          </tr>
        `;
      });
    }

    // PRESUPUESTOS Y DETECCIÓN DE EXCESOS
    function renderBudgets() {
      const grid = document.getElementById('budgets-grid');
      grid.innerHTML = '';

      const now = new Date();
      const currentYM = `${now.getFullYear()}-${String(now.getMonth() + 1).padStart(2, '0')}`;

      let exceededCount = 0;

      state.budgets.forEach(b => {
        const spent = state.transactions
          .filter(t => t.type === 'expense' && t.category.toLowerCase() === b.category.toLowerCase() && t.date && t.date.startsWith(currentYM))
          .reduce((acc, t) => acc + parseFloat(t.amount), 0);

        const limit = parseFloat(b.limit);
        const pct = Math.min(100, Math.round((spent / limit) * 100));
        const isExceeded = spent > limit;

        if (isExceeded) exceededCount++;

        let colorClass = 'bg-emerald-500';
        let badgeHtml = `<span class="text-xs text-slate-400 font-medium">${pct}% consumido</span>`;

        if (pct > 80 && !isExceeded) {
          colorClass = 'bg-amber-500';
        }
        if (isExceeded) {
          colorClass = 'bg-rose-600';
          const over = spent - limit;
          badgeHtml = `<span class="text-xs font-bold text-rose-600 bg-rose-100 px-2.5 py-0.5 rounded-full">⚠️ Excedido por ${formatCurrency(over)}</span>`;
        }

        const icon = getCategoryIcon(b.category);

        grid.innerHTML += `
          <div class="bg-white p-5 rounded-xl shadow-sm border ${isExceeded ? 'border-rose-300 bg-rose-50/20' : 'border-slate-200'} space-y-3 transition">
            <div class="flex justify-between items-center">
              <h3 class="font-bold text-slate-800 text-base">${icon} ${b.category}</h3>
              <button onclick="deleteBudget('${b.id}')" class="text-slate-300 hover:text-rose-500"><i class="fa-solid fa-trash"></i></button>
            </div>
            <div class="flex justify-between text-xs text-slate-500">
              <span>Gastado este mes: <strong class="${isExceeded ? 'text-rose-600 font-bold' : 'text-slate-700'}">${formatCurrency(spent)}</strong></span>
              <span>Límite: <strong class="text-slate-700">${formatCurrency(limit)}</strong></span>
            </div>
            <div class="w-full bg-slate-100 rounded-full h-2.5 overflow-hidden">
              <div class="${colorClass} h-2.5 rounded-full transition-all duration-500" style="width: ${pct}%"></div>
            </div>
            <div class="flex justify-between items-center pt-1">
              ${badgeHtml}
            </div>
          </div>
        `;
      });

      const warningBanner = document.getElementById('budgets-warning-banner');
      if (warningBanner) {
        if (exceededCount > 0) {
          warningBanner.classList.remove('hidden');
          document.getElementById('budgets-warning-text').textContent = `Atención: Tienes ${exceededCount} categoría(s) que sobrepasan el límite de gasto este mes.`;
        } else {
          warningBanner.classList.add('hidden');
        }
      }
    }

    function checkBudgetExceeded(category, txDate) {
      if (!category || !txDate) return;
      const ym = txDate.substring(0, 7);
      const budget = state.budgets.find(b => b.category.toLowerCase() === category.toLowerCase());
      
      if (!budget) return;

      const monthSpent = state.transactions
        .filter(t => t.type === 'expense' && t.category.toLowerCase() === category.toLowerCase() && t.date && t.date.startsWith(ym))
        .reduce((acc, t) => acc + parseFloat(t.amount), 0);

      const limit = parseFloat(budget.limit);

      if (monthSpent > limit) {
        const over = monthSpent - limit;
        const icon = getCategoryIcon(category);
        
        document.getElementById('alert-budget-cat').textContent = `${icon} ${category}`;
        document.getElementById('alert-budget-limit').textContent = formatCurrency(limit);
        document.getElementById('alert-budget-spent').textContent = formatCurrency(monthSpent);
        document.getElementById('alert-budget-over').textContent = `+ ${formatCurrency(over)}`;
        document.getElementById('alert-budget-msg').textContent = `Tus gastos en ${category} para el mes de ${getMonthName(ym)} superaron el presupuesto asignado.`;
        
        openModal('modal-alerta-presupuesto');
      }
    }

    // METAS
    function renderGoals() {
      const grid = document.getElementById('goals-grid');
      grid.innerHTML = '';

      state.goals.forEach(g => {
        const pct = Math.min(100, Math.round((g.currentAmount / g.targetAmount) * 100));

        grid.innerHTML += `
          <div class="bg-white p-5 rounded-xl shadow-sm border border-slate-200 space-y-3">
            <div class="flex justify-between items-center">
              <h3 class="font-bold text-slate-800">${g.name}</h3>
              <button onclick="deleteGoal('${g.id}')" class="text-slate-300 hover:text-rose-500"><i class="fa-solid fa-trash"></i></button>
            </div>
            <p class="text-2xl font-bold text-indigo-600">${formatCurrency(g.currentAmount)} <span class="text-xs text-slate-400 font-normal">de ${formatCurrency(g.targetAmount)}</span></p>
            <div class="w-full bg-slate-100 rounded-full h-2.5 overflow-hidden">
              <div class="bg-indigo-600 h-2.5 rounded-full" style="width: ${pct}%"></div>
            </div>
            <div class="flex justify-between items-center pt-2">
              <span class="text-xs text-slate-400 font-medium">${pct}% completado</span>
              <button onclick="openGoalDepositModal('${g.id}')" class="text-xs bg-indigo-50 text-indigo-600 font-semibold px-3 py-1.5 rounded-lg hover:bg-indigo-100 transition">+ Modificar</button>
            </div>
          </div>
        `;
      });
    }

    function openGoalDepositModal(goalId) {
      document.getElementById('goal-deposit-id').value = goalId;
      document.getElementById('goal-deposit-amount').value = '';
      openModal('modal-aporte-meta');
    }

    function saveGoalContribution(e) {
      e.preventDefault();
      const goalId = document.getElementById('goal-deposit-id').value;
      const action = document.getElementById('goal-action-type').value;
      const amount = parseFloat(document.getElementById('goal-deposit-amount').value);

      if (!amount || isNaN(amount)) return;

      const goal = state.goals.find(g => g.id === goalId);
      if (goal) {
        if (action === 'deposit') {
          goal.currentAmount += amount;
        } else {
          goal.currentAmount = Math.max(0, goal.currentAmount - amount);
        }
        saveData();
      }
      closeModal('modal-aporte-meta');
    }

    // REPORTES Y EXPORTACIÓN
    function populateReportMonthDropdown() {
      const select = document.getElementById('select-report-month');
      if (!select) return;

      const currentVal = select.value;
      const monthsSet = new Set();
      
      const now = new Date();
      const currentYM = `${now.getFullYear()}-${String(now.getMonth() + 1).padStart(2, '0')}`;
      monthsSet.add(currentYM);

      state.transactions.forEach(t => {
        if (t.date && t.date.length >= 7) {
          const ym = t.date.substring(0, 7);
          if (ym.match(/^\d{4}-\d{2}$/)) monthsSet.add(ym);
        }
      });

      const sortedMonths = Array.from(monthsSet).sort().reverse();

      select.innerHTML = '<option value="all">Todo el Histórico</option>';
      sortedMonths.forEach(ym => {
        select.innerHTML += `<option value="${ym}">${getMonthName(ym)}</option>`;
      });

      if (currentVal && Array.from(select.options).some(o => o.value === currentVal)) {
        select.value = currentVal;
      } else {
        select.value = sortedMonths[0] || 'all';
      }
    }

    function renderReports() {
      populateReportMonthDropdown();

      const select = document.getElementById('select-report-month');
      const selectedMonth = select ? select.value : 'all';
      
      document.getElementById('rep-selected-month-label').textContent = getMonthName(selectedMonth);

      let filteredTx = state.transactions;
      if (selectedMonth !== 'all') {
        filteredTx = state.transactions.filter(t => t.date && t.date.startsWith(selectedMonth));
      }

      const monthIncome = filteredTx.filter(t => t.type === 'income').reduce((acc, t) => acc + parseFloat(t.amount), 0);
      const monthExpense = filteredTx.filter(t => t.type === 'expense').reduce((acc, t) => acc + parseFloat(t.amount), 0);
      const monthBalance = monthIncome - monthExpense;

      document.getElementById('rep-month-income').textContent = formatCurrency(monthIncome);
      document.getElementById('rep-month-expense').textContent = formatCurrency(monthExpense);
      
      const balanceEl = document.getElementById('rep-month-balance');
      balanceEl.textContent = formatCurrency(monthBalance);
      balanceEl.className = `text-2xl font-bold mt-1 ${monthBalance >= 0 ? 'text-slate-900' : 'text-rose-600'}`;

      const monthlyData = {};
      state.transactions.forEach(t => {
        if (!t.date || t.date.length < 7) return;
        const ym = t.date.substring(0, 7);
        if (!monthlyData[ym]) monthlyData[ym] = { income: 0, expense: 0 };
        
        if (t.type === 'income') monthlyData[ym].income += parseFloat(t.amount);
        if (t.type === 'expense') monthlyData[ym].expense += parseFloat(t.amount);
      });

      const sortedYMKeys = Object.keys(monthlyData).sort();
      const labelsHist = sortedYMKeys.map(ym => getMonthName(ym));
      const incomeHistData = sortedYMKeys.map(ym => monthlyData[ym].income);
      const expenseHistData = sortedYMKeys.map(ym => monthlyData[ym].expense);

      const ctxHist = document.getElementById('chartHistorico').getContext('2d');
      if (chartHistInstance) chartHistInstance.destroy();

      chartHistInstance = new Chart(ctxHist, {
        type: 'bar',
        data: {
          labels: labelsHist.length ? labelsHist : ['Sin registros'],
          datasets: [
            { label: 'Ingresos 💵', data: incomeHistData.length ? incomeHistData : [0], backgroundColor: '#10b981', borderRadius: 6 },
            { label: 'Gastos 💸', data: expenseHistData.length ? expenseHistData : [0], backgroundColor: '#f43f5e', borderRadius: 6 }
          ]
        },
        options: {
          responsive: true,
          maintainAspectRatio: false,
          plugins: { legend: { position: 'top' } },
          scales: { y: { beginAtZero: true } }
        }
      });

      const expByCat = {};
      filteredTx.filter(t => t.type === 'expense').forEach(t => {
        expByCat[t.category] = (expByCat[t.category] || 0) + parseFloat(t.amount);
      });

      const catLabels = Object.keys(expByCat);
      const catValues = Object.values(expByCat);
      const catLabelsWithIcons = catLabels.map(c => `${getCategoryIcon(c)} ${c}`);

      const ctxRepCat = document.getElementById('chartReporteCategoria').getContext('2d');
      if (chartRepCatInstance) chartRepCatInstance.destroy();

      chartRepCatInstance = new Chart(ctxRepCat, {
        type: 'doughnut',
        data: {
          labels: catLabelsWithIcons.length ? catLabelsWithIcons : ['Sin gastos'],
          datasets: [{
            data: catValues.length ? catValues : [1],
            backgroundColor: catValues.length ? ['#f43f5e', '#6366f1', '#06b6d4', '#f59e0b', '#10b981', '#8b5cf6', '#ec4899'] : ['#e2e8f0']
          }]
        },
        options: {
          responsive: true,
          maintainAspectRatio: false,
          plugins: { legend: { position: 'bottom' } }
        }
      });

      const listEl = document.getElementById('rep-category-list');
      listEl.innerHTML = '';

      if (catLabels.length === 0) {
        listEl.innerHTML = '<p class="text-xs text-slate-400 py-4 text-center">No hay gastos en este período.</p>';
      } else {
        const totalExp = catValues.reduce((a, b) => a + b, 0);
        catLabels.forEach(cat => {
          const val = expByCat[cat];
          const pct = totalExp > 0 ? Math.round((val / totalExp) * 100) : 0;
          const icon = getCategoryIcon(cat);
          listEl.innerHTML += `
            <div class="py-3 flex items-center justify-between">
              <div>
                <p class="text-sm font-semibold text-slate-800">${icon} ${cat}</p>
                <p class="text-xs text-slate-400">${pct}% del total gastado</p>
              </div>
              <p class="text-sm font-bold text-rose-600">${formatCurrency(val)}</p>
            </div>
          `;
        });
      }
    }

    function exportCSV() {
      if (!state.transactions.length) {
        alert("No hay transacciones para exportar.");
        return;
      }

      let csv = 'Fecha,Tipo,Descripcion,Categoria,Cuenta,Monto\n';
      state.transactions.forEach(t => {
        const acc = state.accounts.find(a => a.id === t.accountId);
        const accName = acc ? acc.name : 'N/A';
        csv += `"${t.date}","${t.type}","${t.description.replace(/"/g, '""')}","${t.category}","${accName}",${t.amount}\n`;
      });

      const blob = new Blob([csv], { type: 'text/csv;charset=utf-8;' });
      const url = URL.createObjectURL(blob);
      const link = document.createElement('a');
      link.setAttribute('href', url);
      link.setAttribute('download', `reporte_finanzas_${new Date().toISOString().split('T')[0]}.csv`);
      document.body.appendChild(link);
      link.click();
      document.body.removeChild(link);
    }

    // EDICIÓN Y CREACIÓN DE TRANSACCIONES
    function editTransaction(id) {
      const tx = state.transactions.find(t => t.id === id);
      if (!tx) return;

      document.getElementById('tx-edit-id').value = tx.id;
      document.getElementById('modal-tx-title').textContent = 'Editar Movimiento';

      document.getElementById('tx-type').value = tx.type;
      updateTxCategoryDropdown();
      document.getElementById('tx-category').value = tx.category;

      document.getElementById('tx-amount').value = tx.amount;
      document.getElementById('tx-desc').value = tx.description;
      document.getElementById('tx-account').value = tx.accountId;
      document.getElementById('tx-date').value = tx.date;

      openModal('modal-transaccion');
    }

    function addTransaction(e) {
      e.preventDefault();
      const editId = document.getElementById('tx-edit-id').value;
      const type = document.getElementById('tx-type').value;
      const amount = parseFloat(document.getElementById('tx-amount').value);
      const description = document.getElementById('tx-desc').value;
      const category = document.getElementById('tx-category').value;
      const accountId = document.getElementById('tx-account').value;
      const date = document.getElementById('tx-date').value;

      if (!category) {
        alert("Por favor selecciona una categoría válida.");
        return;
      }

      if (editId) {
        const tx = state.transactions.find(t => t.id === editId);
        if (tx) {
          const oldAcc = state.accounts.find(a => a.id === tx.accountId);
          if (oldAcc) {
            oldAcc.balance += (tx.type === 'income' ? -tx.amount : tx.amount);
          }

          const oldCategory = tx.category;

          tx.type = type;
          tx.amount = amount;
          tx.description = description;
          tx.category = category;
          tx.accountId = accountId;
          tx.date = date;

          const newAcc = state.accounts.find(a => a.id === accountId);
          if (newAcc) {
            newAcc.balance += (type === 'income' ? amount : -amount);
          }

          saveData();
          closeModal('modal-transaccion');

          if (type === 'expense') {
            checkBudgetExceeded(category, date);
            if (oldCategory !== category) {
              checkBudgetExceeded(oldCategory, date);
            }
          }
        }
      } else {
        const account = state.accounts.find(a => a.id === accountId);
        if (account) {
          account.balance += (type === 'income' ? amount : -amount);
        }

        state.transactions.push({ id: 'tx_' + Date.now(), type, amount, description, category, accountId, date });
        saveData();
        closeModal('modal-transaccion');

        if (type === 'expense') {
          checkBudgetExceeded(category, date);
        }
      }
    }

    function addAccount(e) {
      e.preventDefault();
      const name = document.getElementById('acc-name').value;
      const type = document.getElementById('acc-type').value;
      const balance = parseFloat(document.getElementById('acc-balance').value);

      state.accounts.push({ id: 'acc_' + Date.now(), name, type, balance });
      saveData();
      closeModal('modal-cuenta');
      e.target.reset();
    }

    function addBudget(e) {
      e.preventDefault();
      const category = document.getElementById('bg-category').value;
      const limit = parseFloat(document.getElementById('bg-limit').value);

      const existingIdx = state.budgets.findIndex(b => b.category.toLowerCase() === category.toLowerCase());
      if (existingIdx >= 0) {
        state.budgets[existingIdx].limit = limit;
      } else {
        state.budgets.push({ id: 'b_' + Date.now(), category, limit });
      }

      saveData();
      closeModal('modal-presupuesto');
      e.target.reset();

      const today = new Date().toISOString().split('T')[0];
      checkBudgetExceeded(category, today);
    }

    function addGoal(e) {
      e.preventDefault();
      const name = document.getElementById('gl-name').value;
      const targetAmount = parseFloat(document.getElementById('gl-target').value);
      const currentAmount = parseFloat(document.getElementById('gl-current').value);

      state.goals.push({ id: 'g_' + Date.now(), name, targetAmount, currentAmount });
      saveData();
      closeModal('modal-meta');
      e.target.reset();
    }

    function deleteTransaction(id) {
      const tx = state.transactions.find(t => t.id === id);
      if (tx) {
        const acc = state.accounts.find(a => a.id === tx.accountId);
        if (acc) {
          acc.balance += (tx.type === 'income' ? -tx.amount : tx.amount);
        }
      }
      state.transactions = state.transactions.filter(t => t.id !== id);
      saveData();
    }

    function deleteAccount(id) {
      state.accounts = state.accounts.filter(a => a.id !== id);
      saveData();
    }

    function deleteBudget(id) {
      state.budgets = state.budgets.filter(b => b.id !== id);
      saveData();
    }

    function deleteGoal(id) {
      state.goals = state.goals.filter(g => g.id !== id);
      saveData();
    }
  </script>
</body>
</html>

