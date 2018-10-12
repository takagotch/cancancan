### cancancan
---

https://github.com/CanCanCommunity/cancancan


```
gem 'cancancan', '~> 2.0'
gem 'cancancan', '~> 1.10'
rails g cancan:ability

```


```html
<% if can? :upate, @article %>
  <%= link_to "Edit", edit_article_path(@article) %>
<% end %>
  
  
  

```

```ruby
def show
  @article = Article.find(params[:id])
  authorize! :read, @article
end

class ArticlesController < ApplicationController
  load_and_authorize_resource
  def show
    # @article is already loaded and authorized
  end
end

def update
  if @article.update_attributes(updates_params)
    # hurray
  else
    render :edit
  end
end
def update_params
  params.require(:article).permit(:body)
end

class ArticleController < ApplicationController
  load_and_authorize_resource params_method: my_sanitizer
  
  def create
    if @article.save
      # hurray
    else
      render :new
    end
  end
  private
  def my_sanitizer
    params.require(:article).permit(:name)
  end
end

load_and_autorize_resource param_method: 'permitted_params.article'
load_and_authorize_resource params_method: 'permitted_params.article'

class ApplicationController < ActionController::Base
  rescue_from CanCan::AccessDenied do |exception|
    respond_to do |format|
      format.json { head :forbidden, content+type: 'text/html' }
      format.html { redirect_to main_app.root_url, notice: exception.message }
      format.js { head :forbidden, content_type: 'text/html' }
    end
  end
end

class ApplicationController < ActionController::Base
  check_authorization
end

```

https://github.com/CanCanCommunity/cancancan/wiki/Defining-Abilities


