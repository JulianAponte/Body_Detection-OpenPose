# 🤝 Contribuir a Body Detection OpenPose

Gracias por tu interés en contribuir. Esta guía te ayudará a hacerlo correctamente.

---

## 📋 Código de Conducta

- Sé respetuoso con otros contribuidores
- Acepta crítica constructiva
- Enfócate en lo mejor para la comunidad
- Reporta comportamiento inapropiado

---

## 🚀 Cómo Contribuir

### 1. Fork y Clona

```bash
# Fork el repositorio en GitHub

# Clona tu fork
git clone https://github.com/tu-usuario/Body_Detection-OpenPose.git
cd Body_Detection-OpenPose

# Agrega upstream
git remote add upstream https://github.com/JulianAponte/Body_Detection-OpenPose.git
```

### 2. Crea una Rama de Feature

```bash
# Actualiza main
git fetch upstream
git checkout main
git merge upstream/main

# Crea tu rama
git checkout -b feature/tu-feature-nombre
```

**Convenciones de nombres:**
- `feature/descripcion-corta` - Nuevas características
- `fix/descripcion-corta` - Bug fixes
- `docs/descripcion-corta` - Documentación
- `refactor/descripcion-corta` - Cambios de código

### 3. Desarrolla tu Cambio

```bash
# Realiza tus cambios
# Prueba localmente

# Si es frontend
npm run dev
npm test

# Si es backend
cd body-cam
pytest tests/
```

### 4. Commit y Push

```bash
# Commit con mensaje descriptivo
git commit -m "feat: agregar nueva feature X"

# Push a tu fork
git push origin feature/tu-feature-nombre
```

**Formato de commits:**
```
<tipo>: <descripción corta>

<descripción detallada opcional>

Fixes #123
```

Tipos válidos:
- `feat` - Nueva característica
- `fix` - Bug fix
- `docs` - Cambios en documentación
- `style` - Cambios de formato
- `refactor` - Refactorización
- `test` - Tests
- `chore` - Otros cambios

### 5. Envía un Pull Request

1. Ve a GitHub y crea Pull Request
2. Describe los cambios claramente
3. Referencia issues relacionados
4. Espera revisión

---

## 📝 Directrices de Código

### Frontend (TypeScript/React)

✅ **Requerido:**
- Type safety con TypeScript
- Componentes funcionales con hooks
- Props interfaces
- Comments en lógica compleja

### Backend (Python)

✅ **Requerido:**
- Type hints en funciones
- Docstrings en funciones
- Snake_case para funciones
- PascalCase para clases

---

## 🧪 Testing

### Frontend

```bash
npm test
npm run test:coverage
```

### Backend

```bash
cd body-cam
python -m pytest tests/ -v
pytest tests/ --cov=.
```

---

## 📚 Referencias

- [README.md](README.md) - Visión general
- [ARCHITECTURE.md](ARCHITECTURE.md) - Arquitectura técnica
- [STRUCTURE.md](STRUCTURE.md) - Estructura del proyecto

---

**¡Gracias por contribuir! 🎉**
