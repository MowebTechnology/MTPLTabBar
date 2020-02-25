# MTPLTabBar

## Overview

Using MTPLTabBar you can build a tabBar view controller with totally customized cells

## Installing pod
`pod 'MTPLTabBar'`

## Initial configuration

### 1. Create a ViewController that will be parent of TabBar
### 2. Implement MTPLTabBarViewDelegate protocol from MTPLTabBar

> After doing above process you have to follow below code


	class TabBarController: BaseViewController, MTPLTabBarViewDelegate {
    
   	 var tabBarViewControllers: [UIViewController]? = {
	        // Create your view controller for tabs here and return
	        
	        let vc1: UIViewController = UIViewController()
	        vc1.backgroundColor = .red
	        
			let vc2: UIViewController = UIViewController()
	        vc2.backgroundColor = .green
	        
			let vc3: UIViewController = UIViewController()
	      	 vc3.backgroundColor = .blue
	      	 
			let vc4: UIViewController = UIViewController()
	        vc4.backgroundColor = .yellow
		        
		        
		    return [vc1, vc2, vc3, vc4]
	    }()
     
    
    	// Like this you define MTPLTabBarView instance 
    	var tabBarView: MTPLTabBarView!
    
	    override func viewDidLoad() {
	        super.viewDidLoad()
	        tabBarView = MTPLTabBarView()
	        tabBarView.bottmTabViewHeight = 50
	        tabBarView.mtplTabBarDelegate = self
	        tabBarView.register(UINib(nibName: String(describing: TabBarCell.self), bundle: nil), forCellWithReuseIdentifier: "TabBarCell")
	        
	        tabBarView.setupAndPresentTabBar(selectedTab: 0, mtplTabbarView: tabBarView)
	     }
	}
	
	extension TabBarController {
     
	    func tabBarViewController(_ collectionView: UICollectionView, cellForItemAt indexPath: IndexPath, isSelected: Bool) -> UICollectionViewCell {
	        let cell = collectionView.dequeueReusableCell(withReuseIdentifier: "TabBarCell", for: indexPath) as! TabBarCell
	        
	        if let currentVC = tabBarViewControllers?[safe: indexPath.item] {
	            cell.tabImageView.image = isSelected ? currentVC.tabImageSelected : currentVC.tabImage
	        } else {
	            cell.tabImageView.image = nil
	        }
	        
	        return cell
	    }
	    
	    func tabBarViewController(_ collectionView: UICollectionView, layout collectionViewLayout: UICollectionViewLayout, sizeForItemAt indexPath: IndexPath) -> CGSize {

	    }
	    
	    func tabBarViewController(didPresentControllerAt index: Int) {
	   	 
	   	}
	    
	    func tabBarInterItemSpacing(defaultProperty: CGFloat) -> CGFloat {
	        return defaultInterItemSpacing
	    }
	    
	    func tabBarViewEdgeInsets(defaultProperty: UIEdgeInsets) -> UIEdgeInsets {
	        return defaultProperty
	    }
	    
	    func tabBarBackgroundColor(defaultProperty: UIColor) -> UIColor {
	        return defaultProperty
	    }
}

> By doing above configuration your viewcontroller will present tabs


## Usage

* By code you can change selected tab

		self.navigationController?.mtplTabBarView?.setSelectedTab(0)
* Showing TabBar

		self.mtplTabBarView?.showTabBar()
* Hide TabBar

		self.mtplTabBarView?.hideTabBar(completion: {
		// now you perform something
		}
