# 📚 Siakit Docs e Design System

---

## 🧱 **Flex**
O componente **Flex** é usado para criar layouts flexíveis e responsivos.

### Principais Propriedades:
- **`flex`**: Define se o elemento ocupa todo o espaço disponível.
- **`direction`**: Direção do flexbox (`"row"`, `"column"`).
- **`gap`**: Espaçamento entre os elementos.
- **`align`**: Alinhamento vertical (`"start"`, `"center"`, `"end"`).
- **`justify`**: Alinhamento horizontal (`"start"`, `"center"`, `"end"`, `"between"`, etc).
- **`padding`**: Adiciona padding interno.
- **`overflow`**: Controla o comportamento de overflow.
- **`css{{}}`**: Para especificar seu próprio estilo baseado em css (geralmente tem em todos os componentes siakit)
- Outros... (Ctrl + Espaço para saber todos)

### Exemplo de Uso:
```jsx
import { Flex } from '@siakit/layout'

<Flex flex direction="column" gap padding align="center" justify="center">
    {/* Conteúdo */}
</Flex>
```

---

## 🃏 **Card**
O componente **Card** é usado para criar contêineres destacados com bordas arredondadas.

### Exemplo de Uso:
```jsx
import { Card } from '@siakit/card'

    <Card width="240px" direction="column">
      {/* Conteúdo do card */}
    </Card>
```

---

## 📊 **Table**
O componente **Table** exibe dados tabulares com funcionalidades avançadas.

### Principais Propriedades:
- **`data`**: Array de objetos com os dados da tabela.
- **`headers`**: Configuração dos cabeçalhos.
- **`actions`**: Ações disponíveis para cada linha.
- **`onClick`**: Função chamada ao clicar em uma linha.

#### Estrutura do Header:
```typescript
type HeaderType = {
  label: string;
  dataIndex: string;
  sort?: string | null;
  visible?: boolean;
  align?: 'left' | 'right';
  render?: (data: RenderType) => React.ReactNode;
}
```

### Exemplo de Uso:
```jsx
import { Table } from '@siakit/table'

function handleEdit(item) {
  console.log('Editar:', item)
}

function handleDelete(item) {
  console.log('Excluir:', item)
}

const data = [
  { id: 1, name: 'João', email: 'joao@example.com' },
  { id: 2, name: 'Maria', email: 'maria@example.com' }
]

export function TableExample() {
  return (
    <Table 
      data={data}
      headers={[
        { label: 'ID', dataIndex: 'id' },
        { label: 'Nome', dataIndex: 'name' },
        { 
          label: 'E-mail', 
          dataIndex: 'email',
          render: ({ value }) => <a href={`mailto:${value}`}>{value}</a>
        },
      ]}
      actions={[
        {
          label: 'Editar',
          onClick: (item) => handleEdit(item)
        },
        {
          label: 'Excluir',
          type: 'danger',
          onClick: (item) => handleDelete(item)
        }
      ]}
    />
  )
}
```

---

## 🔢 **Pagination**
Componente usado para navegação entre páginas em listas de dados.

### Principais Propriedades:
- **`currentPage`**: Página atual.
- **`perPage`**: Itens por página.
- **`total`**: Total de itens.
- **`onPageChange`**: Função chamada ao mudar de página.
- **`onPerPageChange`**: Função chamada ao alterar itens por página.

### Exemplo de Uso:
```jsx
import { Pagination } from '@siakit/pagination'

export function PaginationExample() {
  const [currentPage, setCurrentPage] = useState(1)
  const [perPage, setPerPage] = useState(10)
  const totalCount = 100

  return (
    <Pagination
      currentPage={currentPage}
      perPage={perPage}
      total={totalCount}
      onPageChange={setCurrentPage}
      onPerPageChange={setPerPage}
    />
  )
}
```

---

## 📋 **FormProvider e React Hook Form**
Utiliza o **React Hook Form** para gerenciar formulários com validação.

### Exemplo de Uso:
```jsx
import { useForm, FormProvider } from 'react-hook-form'
import { z } from 'zod'
import { zodResolver } from '@hookform/resolvers/zod'
import { TextInput, Select } from '@siakit/react-hook-form'
import { Button } from '@siakit/button'
import { Footer } from '@siakit/footer'

// Definindo o schema de validação com zod
const schema = z.object({
  name: z.string().min(2, 'Nome muito curto'),
  email: z.string().email('Email inválido'),
  profileType: z.number()
})

// Função exemplo de cancelar
function handleCancel() {
  console.log('Cancelado')
}

export function MyForm() {
  const methods = useForm({
    resolver: zodResolver(schema),
    defaultValues: {
      name: '',
      email: '',
      profileType: null
    }
  })

  const { handleSubmit } = methods

  function onSubmit(data) {
    console.log(data)
  }

  return (
    <FormProvider {...methods}>
        <Flex as="form" direction="column" gap padding onSubmit={handleSubmit(onSubmit)}>
          <TextInput name="name" label="Nome" />
          <TextInput name="email" label="Email" />
          <Select 
            name="profileType" 
            label="Tipo de Perfil"
            options={[
              { value: 1, label: 'Administrador' },
              { value: 2, label: 'Usuário' }
            ]} 
          />
          <Footer>
            <Button type="button" variant="ghost" onClick={handleCancel}>Cancelar</Button>
            <Button type="submit">Salvar</Button>
          </Footer>
        </Flex>
    </FormProvider>
  )
}
```

---

## 🛠️ **Outros Componentes**

### **Inputs**
- **TextInput**:  
  ```jsx
  import { TextInput } from '@siakit/react-hook-form'
  // Exemplo:
  <TextInput name="name" label="Nome" />
  ```

- **Select**:  
  ```jsx
  import { Select } from '@siakit/react-hook-form'
  // Exemplo:
  <Select 
    name="category" 
    label="Categoria" 
    options={[
      { value: 1, label: 'Categoria 1' },
      { value: 2, label: 'Categoria 2' }
    ]} 
  />
  ```

- **MoneyInput**:  
  ```jsx
  import { MoneyInput } from '@siakit/react-hook-form'
  // Exemplo:
  <MoneyInput name="price" label="Preço" />
  ```

- **NumberInput**:  
  ```jsx
  import { NumberInput } from '@siakit/react-hook-form'
  // Exemplo:
  <NumberInput name="quantity" label="Quantidade" />
  ```

- **TextAreaInput**:  
  ```jsx
  import { TextAreaInput } from '@siakit/react-hook-form'
  // Exemplo:
  <TextAreaInput name="description" label="Descrição" />
  ```

- **DatePicker**:  
  ```jsx
  import { DatePicker } from '@siakit/react-hook-form'
  // Exemplo:
  <DatePicker name="date" label="Data" />
  ```

- **Switch**:  
  ```jsx
  import { Switch } from '@siakit/react-hook-form'
  // Exemplo:
  <Switch name="active" label="Ativo" />
  ```

- **PhoneInput**:  
  ```jsx
  import { PhoneInput } from '@siakit/react-hook-form'
  // Exemplo:
  <PhoneInput name="phone" label="Telefone" />
  ```

---

### **Modais**
```jsx
import React, { useState } from 'react'
import { Button } from '@siakit/button'
import { Modal, ModalContent } from '@siakit/modal'
import { Flex } from '@siakit/layout'
import { Footer } from '@siakit/footer'

export function ModalExample() {
  const [isOpen, setIsOpen] = useState(false)

  function handleConfirm() {
    console.log('Confirmado')
  }

  return (
    <>
      <Button onClick={() => setIsOpen(true)}>
        Abrir Modal
      </Button>
      
      <Modal open={isOpen} onOpenChange={setIsOpen}>
        <ModalContent title="Título do Modal" size="md">
          <Flex padding direction="column" gap>
            {/* Conteúdo do modal */}
            <Footer>
              <Button variant="ghost" onClick={() => setIsOpen(false)}>
                Cancelar
              </Button>
              <Button onClick={handleConfirm}>
                Confirmar
              </Button>
            </Footer>
          </Flex>
        </ModalContent>
      </Modal>
    </>
  )
}
```

---

### **Grid**
```jsx
import React from 'react'
import { Grid, Flex } from '@siakit/layout'
import { Card } from '@siakit/card'

export function GridExample() {
  return (
    <Grid columns={2} gap>
      <Card>
        {/* Conteúdo */}
      </Card>
      <Card>
        {/* Conteúdo */}
      </Card>
    </Grid>
  )
}
```

---

### **Outros**
- **Badge**:  
  ```jsx
  import { Badge } from '@siakit/badge'
  // Exemplo:
  <Badge color="green">Ativo</Badge>
  <Badge color="red">Inativo</Badge>
  ```

- **Button**:  
  ```jsx
  import { Button } from '@siakit/button'
  // Exemplo:
  <Button onClick={() => console.log('Clicado')}>Clique aqui</Button>
  <Button variant="ghost" colorScheme="gray">Cancelar</Button>
  <Button variant="secondary">Secundário</Button>
  ```

- **Text**:  
  ```jsx
  import { Text } from '@siakit/text'
  // Exemplo:
  <Text>Texto normal</Text>
  <Text size="lg">Texto grande</Text>
  <Text size="sm">Texto pequeno</Text>
  ```

- **Separator**:  
  ```jsx
  import { Separator } from '@siakit/separator'
  // Exemplo:
  <Flex direction="column">
    <Text>Conteúdo acima</Text>
    <Separator />
    <Text>Conteúdo abaixo</Text>
  </Flex>

  // Ou mudando a direção
  <Separator direction="horizontal" />
  <Separator />
  <Separator direction="vertical" />
  ```

- **Heading**:  
  ```jsx
  import { Heading } from '@siakit/heading'
  // Exemplo:
  <Heading size="lg">Título da Página grande</Heading>
  <Heading>Título da Página médio</Heading>
  <Heading size="sm">Título da Página pequeno</Heading>
  <Heading size="xs">Título da Página extra pequeno</Heading>
  ```

- **useDialog**:  
  ```jsx
  import { useDialog } from '@siakit/dialog'

  const { addDialog } = useDialog()

  function handleDelete() {
    addDialog({
    type: 'danger', // info, success, warning, danger
    title: 'Excluir item',
    actionText: 'Excluir',
    cancelText: 'Cancelar',
    description: 'Você tem certeza que deseja excluir este item?',
    onCancel: () => console.log('Cancelado'),
    onAction: () => console.log('Item excluído')
    })
  }
  ```

- **useLoading**:  
  ```jsx
  import { useLoading } from '@siakit/loading'

  const { setLoading } = useLoading()

  async function fetchData() {
    setLoading(true)
    try {
      // chamada assíncrona
    } finally {
      setLoading(false)
    }
  }
  ```

 - **Props — `css={{}}` e cores**

   1. Tokens de cor
     - Existem os tokens do tema, por exemplo: `$gray6`, `$white`, `$primary` ou tokens de sombra como `$lg`. Esses tokens mantêm a aparência consistente com o design system.
     - Use variáveis CSS globais (`var(--colors-...)`) apenas quando precisar acessar ou sobrescrever valores expostos globalmente (por exemplo: `var(--colors-red10)`).

   2. Prop `css={{}}`
     - Muitos componentes aceitam `css={{ ... }}` para customização localizada.
     - Prefira não modificar tanto o componente já que ele tem um modelo próprio e use o css para coisas especificas.
     - Exemplos:

     ```jsx
     <Heading size="xxs" css={{ color: '$white' }}>Título</Heading>
     <Card css={{ backgroundColor: '$gray6' }}>Conteúdo</Card>
     <Flex css={{ backgroundColor: 'var(--colors-gray9)' }}>...</Flex>
     ```


  
