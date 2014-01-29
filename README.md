# Phoenix
> Realtime Elixir Web Framework

## Goals
- First class websockets
- Ring distribution

## Creating a new Phoenix application

```console
mix phoenix.new you_app /path/to
```

## Usage

```elixir
defmodule Router do
  use Phoenix.Router, port: 4000

  get "pages/:page", PagesController, :show, as: :page
  get "files/*path", FilesController, :show
  get "profiles/user-:id", UsersController, :show
  resources "users", UsersController
end

defmodule PagesController do
  use Phoenix.Controller

  def show(conn) do
    if conn.params["page"] in ["admin"] do
      redirect conn, Router.page_path(page: "unauthorized")
    else
      text conn, "Showing page #{conn.params["page"]}"
    end
  end

end

defmodule UsersController do
  use Phoenix.Controller

  def show(conn) do
    text conn, "Showing user #{conn.params["id"]}"
  end

  def index(conn) do
    html conn, """
    <html>
      <body>
        <h1>Users</h1>
      </body>
    </html>
    """
  end
end
```

## Starting the application

```bash
$ mix run -e 'Router.start' --no-halt mix.exs
```

